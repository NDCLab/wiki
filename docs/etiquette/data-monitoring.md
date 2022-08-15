---
layout: default
title: Data Monitoring
parent: Etiquette
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Central Tracker](#central-tracker)
3. [Protocol](#protocol)
4. [Setting Up](#setting-up)
5. [hallMonitor.sub](#hallmonitor.sub)
6. [preprocess.sub](#preprocess.sub)
7. [Final Considerations](#final-considerations)


## Overview
Data monitoring is an ongoing process during data collection and preprocessing. This process has three key goals:
1. Regularly check that data is in **good order** (e.g., proper organization and correct file naming).
2. Regularly check on data **quality** (e.g., preprocessed data points are not wildly different than expections, implying an error in the study experiment).
3. Maintain an up-to-date **central tracker** with all relevant data points per participant.

At this time, these steps are handled manually by study leads for data collection projects. The long-term goal of the NDCLab, however, is to automate these functions.


## Central Tracker
Each data collection project has a central tracker that provides a real-time overview of what data is available for each participant.

#### File Name
Scripts in the data monitoring ecosystem access a study's central tracker based on its filename. For this reason, the nomenclature is standardized: `central-tracker_dataset-name-without-dataset`. For example, the `memory-for-error-dataset` project has a central tracker named `central-tracker_memory-for-error`.

#### Required Columns
The first two columns in every NDCLab central tracker are the same:
- id (this is the subject ID)
- consent (this connects to the "y/n" of the REDCap consent instrument)

Additionally, the central tracker must have one column for each data type collected. These are synonymous with the subfolders in `sourcedata/raw`:
- redcapData
- pavloviaData or psychopyData
- zoomData and/or audioData and/or videoData

#### Subject IDs
The rows of the first column of the central tracker must be pre-populated with anticipated subject IDs. That is, the data monitoring scripts should not need to "guess" which participants they are looking for. It is ok to pre-populate with many more IDs than you expect to collect, and then delete the extraneous IDs after the close of data collection.


## Protocol
Although the broad strokes of data monitoring are identical across NDCLab studies, each data collection process should establish its own data monitoring protoocl that connects these lab processes with study-specific details. This is also helpful to crystallize the data monitoring actions performed as the defaults within the lab-wide scripts might change over time.


## Setting Up
Once the central tracker and a draft of the data monitoring protocol are prepared, the study lead should begin data monitoring by copying a set of scripts to the dataset.

From the [HPC shell](https://ndclab.github.io/wiki/docs/hpc/accessing.html), navigate to the datasets folder:
```
cd /home/data/NDClab/datasets
```

You will input a single command that indicates which dataset should be set up, which data types are involved, and which PsychoPy/Pavlovia tasks are collected. Here is the core structure of the command:
```
sh /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup-moniprep.sh YOUR-DATASET/ DATA-TYPES PSYCHOPY-TASK-NAME
```
**YOUR-DATASET:** this is the name of your dataset
**DATA-TYPES:** include each data type you have in your `sourcedata/raw` folder, separated by a comma (no space) (redcap, audio, eeg).
**PSYCHOPY-TASK-NAME:** include each PsychoPy task name for which a CSV file will exist per participant

Here is an example of the setup line for readAloud-valence-dataset. It includes three data types: pavlovia, redcap, and zoom. Within Pavlovia, one CSV per participant is expected: read-aloud-val-o_s1_r1_e1.
```
sh /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup-moniprep.sh readAloud-valence-dataset/ pavlovia,redcap,zoom read-aloud-val-o
```

After executing this command, the following new files will be added to your dataset's data-monitoring folder:
- hallMonitor.sh
- hallMonitor.sub
- preprocess.sub
- inst-tracker.py
- rename-cols.py
- update-tracker.py

Details for each are available below.


## hallMonitor.sub

### Purpose
The hallMonitor script checks that raw data (`sourcedata/raw`) is in good order and, once confirmed, places a copy of the data in `sourcedata/checked`. This serves two key purposes:
1. issues with the incoming data (e.g., improper file naming) are identified and corrected early
2. downstream processes interact with the "checked" data and safeguard the integrity of the original "raw" data

Specifically, hallMonitor performs the following checks:
#### REDCap
1. Identifies most recent REDCap CSV.
2. Copies this file to `sourcedata/checked`.
3. Updates the redcapData column in the central tracker, as well as any columns named after a REDCap instrument (such as aq10_s1_r1_e1).

#### Pavlovia/Psychopy
1. Checks folders in `sourcedata/raw/pavlovia` or `sourcedata/raw/psychopy`; if any new files within previously existing folders are found, these files are copied to the existing subject folder in `sourcedata/checked.`
2. Verifies that there is only a single .csv file for each tracked task (that is, there are no duplicate records for a single participant). (If you have a situation where you do have two separate files, zipping one of them will prevent hallMonitor from throwing an error every time you run it.)
3. Checks for the existence of any new subject folders in `sourcedata/raw/pavlovia` or `sourcedata/raw/psychopy` and, if they are found, verifies the correct subject folder nomenclature (i.e., sub-XXXXXX).
4. For correctly-named, new subject folders, the folder is copied over to `sourcedata/checked/pavlovia` or `sourcedata/checked/psychopy`.
5. Updates the pavloviaData or psychopyData column in the central tracker.

If any duplicate files or improper folder names are identified, hallMonitor outputs a red error message.


#### Zoom/Audio/Video
Audio and video files are managed manually by the study lead. Proper encryption should be verified (that is, decryption using the study password should be tested and confirmed), after which the participant's audio/video files should be manually copied to `sourcedata/checked`.  The hallMonitor script verifies the existence of a folder in `sourcedata/checked` and updates the zoomData, audioData, or videoData column of the central tracker accordingly.

#### EEG
(TBD)

### Customize
Most customization required for the hallMonitor script is handled by the setup command above. However, if REDCap column names need to be re-mapped to match the expectations of the instruments script, this can be built directly into hallMonitor. There are two options available:

#### one-to-one mapping
If just the instrument name requires remapping, the `-m` flag allows you to specify this. Here is an example where the mistakenly named "sas" instrument is mapped to "sas2":
![hallmonitor-m-flag](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/hallmonitor-m-flag.png)

#### header replacement
If both the instrument name and the item numbers require remapping, you will use the `-r` flag to replace all column names. You will need to create a comma-separated list of the column names that should be used:
1. Right-click the REDCap .csv file and open with a text editor.
2. Copy the entire first line (careful: this first line may span _visually_ over several lines in the text editor) except for "record_id" onto your clipboard.
3. Insert into hallMonitor.sub following the instructions below.

To modify hallMonitor.sub:
1. Navigate to the data-monitoring folder: `cd your-dataset/data-monitoring`.
2. Open the .sub file: `nano hallMonitor.sub`.
3. Arrow down to the last line (`./hallMonitor.sh`), add a space, then the flag (`-m` or `-r`) and the mapping or replacement details.
4. Save your changes by holding down the ctrl key and pressing the letter 'o'. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return.
5. To exit the nano view, hold down the ctrl key again and press the letter 'x'.

If you have added any modification to the REDCap header, this is executed (by running hallMonitor.sub) via the rename-cols.py script.

#### update-tracker.py
You need to inform hallMonitor which columns it should use to check for the existence of data in the REDCap .csv so that it can update the instrument-specific data points in your central tracker. In general, this is best accomplished with the "timestamp" column in REDCap, which only has data if a participant completed the specific questionnaire. To connect your REDCap data to your central tracker, complete the dictionary in update-tracker.py appropriately. Use the same `nano` command as above. Here is an example where hallMonitor will look for the existence of data for demo_b and bfne_b based on their timestamp:
```
redcheck_columns = {
    "demo_b_s1_r1_e1_timestamp" : "demo_b_s1_r1_e1", 
    "bfne_b_s1_r1_e1_timestamp" : "bfne_b_s1_r1_e1"}
```

### How to Run
The hallMonitor script should be run weekly by the project lead. It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on fridays 'run hallMonitor'`).

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

Review the output for errors requiring correction. After making any necessary corrections, re-run the script until no errors are received, then remove all .out files to keep a tidy folder (`rm slurm-NUMBER.out`).

The hallMonitor script automatically updates the data-monitoring-log.md file in the dataset's data-monitoring folder.


## preprocess.sub

### Purpose
Pre-processing scripts transform the data collected from participants (questionnaires, behavioral tasks) into aggregate numbers that can be used for data analysis. These should draw upon data in the `sourcedata/checked` folder and output to `derivatives/preprocessed`. The preprocess slurm script is a handy shortcut that binds together the automated scoring of REDCap data (via the instruments script) along with any other custom scripts that you tell it to run.

### Instruments
The preprocess slurm script calls the instruments scoring mechanism, which will identify the most recent REDCap file in `sourcedata/checked/redcap`, score it automatically, and output it to `derivatives/preprocessed`, having renamed the "DATA" in the original filename to "SCRD."

### R/MATLAB/Python Scripts
You need to create and test these scripts first on local and individually on the HPC before binding them into preprocess.sub. This is very important because if you accidentally create an infinite loop on the HPC, you could burn through all of the lab's monthly time allottment on the HPC and you would be forced to do all your calculations by hand until the end of the month! :cold_sweat:

The wiki includes instructions for running standalone [R](https://ndclab.github.io/wiki/docs/hpc/r.html), [MATLAB](https://ndclab.github.io/wiki/docs/hpc/matlab.html), and [Python](https://ndclab.github.io/wiki/docs/hpc/python.html) scripts.

In addition to preprocessing your data, your R, MATLAB, or Python scripts must include the necessary code to update your study's central tracker when they run. Here is an example in R that can be modified for your script:
```
#load central tracker
track_path <- '/home/data/NDClab/datasets/readAloud-valence-dataset/data-monitoring/central-tracker_readAloud-valence.csv'
trackerDat <- read.csv(track_path, header=TRUE, check.names=FALSE)

#readAloudDisfluencies_s1_r1_e1
for(row in 1:length(trackerDat$id)){
  id <- trackerDat[row, "id"]
  if (id %in% unique(disfluencySummaryDat$id)){
    trackerDat[trackerDat$id == id, ]$readAloudDisfluencies_s1_r1_e1 = "1"
  } else {
    trackerDat[trackerDat$id == id, ]$readAloudDisfluencies_s1_r1_e1 = "0"
  }
}
print("Updated readAloudDisfluencies_s1_r1_e1!")

#write back to central tracker
write.csv(trackerDat, track_path, row.names = FALSE)
```

### Customize
In addition to creating the preprocessing scripts that are specific to the study, two base scripts must be customized to interconnect the various resources available.

##### preprocess.sub
You must specify the container(s) and script(s) that you want included in the preprocess slurm script. Use the same `nano` command as above to modify the preprocess.sub file contents. Here is an example:
![preprocess-example](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/preprocess-example.png)

##### inst-tracker.py
This script enables the study's central tracker to be updated with the appropriate scored data from the instruments scoring script. Use the same `nano` command as above to fill in the `check-columns` list with the column headers from the central tracker that should be reviewed and updated during the REDCap scoring process. For example, to check for the two scored outputs for the STAI5 instrument, you would use:
```
check_columns = [
    "stai5_scrdS_s1_r1_e1",
    "stai5_scrdT_s1_r1_e1"]
```

### How to Run
Pre-processing scripts should be created as early as possible in the data collection process (ideally to process even the first participant!), and then should be run by the project lead on a weekly basis to ensure that the incoming data appears to be in good order (for instance, we’re not seeing a trend of wild inaccuracy in simple computer tasks or strange numbers in questionnaire data). 

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

The preprocess slurm script automatically updates the data-monitoring-log.md file in the dataset's data-monitoring folder.


## Final Considerations
- If you switch to a new REDCap project during data collection (for instance, because you added a new instrument or corrected an old one), be sure to check any header mapping/replacements you added `hallMonitor.sub` as these may need to be modified or deleted.
- When data collection is complete, you should comment out the lines in `preprocess.sub` that are no longer needed (for example, the lines that trigger the instruments script) so that you don't create unnecessary duplicates.