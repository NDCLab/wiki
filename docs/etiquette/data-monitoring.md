---
layout: default
title: Data Monitoring
parent: Etiquette
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Sourcedata Structure](#sourcedata-structure)
3. [Central Tracker](#central-tracker)
4. [Protocol](#protocol)
5. [Setting Up](#setting-up)
6. [hallMonitor.sub](#hallmonitorsub)
7. [preprocess.sub](#`preprocess.sub`)
8. [Final Considerations](#final-considerations)


## Overview
Data monitoring is an ongoing process during data collection and preprocessing. This process has three key goals:
1. Regularly check that data is in **good order** (e.g., proper organization and correct file naming).
2. Regularly check on data **quality** (e.g., preprocessed data points are not wildly different than expections, implying an error in the study experiment).
3. Maintain an up-to-date **central tracker** with all relevant data points per participant.

At this time, these steps are handled manually by study leads for data collection projects. The long-term goal of the NDCLab, however, is to automate these functions.


## Sourcedata Structure
Within `sourcedata/raw`, folders should be organized as follows (and as appropriate for the data being collected—not all folders will be required for all projects):<br/>
/raw/<br/>
├── redcap/<br/>
├── psychopy/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>


## Central Tracker
Each data collection project has a central tracker that provides a real-time overview of what data is available for each participant.

#### Data Dictionary
The central tracker will be built directly from the contents of the `central-tracker_datadict.csv` file that you create.  The sample template includes instructions within {brackets}.  Consult also the "datadict_definitions.csv" file for details.

#### Required Variables
The first two columns in every NDCLab central tracker are the same:
- id (this is the subject ID), be careful to update the allowedValues information
- consent (this connects to the "y/n" of the REDCap consent instrument)

Additionally, the central tracker must have one column for each data type collected. These basically align with the subfolders in `sourcedata/raw/` (but note that, here, we specify which system was used to collect the data that is stored in the `sourcedata/raw/eeg/` folder):
- audioData
- videoData
- zoomData
- bvData (EEG data collected with the Brain Vision system)
- egiData (EEG data collected with the EGI system)
- digiData

For task data from PsychoPy/Pavlovia, create one row for each individual task, named exactly as the task is (including any session/run/event suffix).  The associated Description cell(s) should begin with "psychopy:".

For questionnaire data from REDCap, create one row for each individual questionnaire, named exactly as the questionnaire is (including any session/run/event suffix). The associated Description cells should begin with "redcap_data:".

For scored data from REDCap questionnaires, create one row for each individual subscore, named exactly as the subscore is (including any session/run/event suffix). The associated Description cells should begin with "redcap_scrd:".

For custom variables, you will control these in your preprocessing scripts.  Be sure to specify how each is operating and include the name of the script in the provenance column.


#### File Name
Scripts in the data monitoring ecosystem access a study's central tracker based on its filename. For this reason, the nomenclature is standardized: `central-tracker_dataset-name`. For example, the `memory-for-error-dataset` project has a central tracker named `central-tracker_memory-for-error-dataset`. You do not need to name this file yourself, but you do need to ensure that the data dictionary you create for your central tracker is named `central-tracker_datadict.csv` and that it lives in `data-monitoring/data-dictionary/` within your dataset repository.


#### Subject IDs
The setup script for data monitoring will prepopulate 1000 IDs based on the numbering convention you specify.  You may delete any that are unnecessary, or add in others at a later date.


## Protocol
Although the broad strokes of data monitoring are identical across NDCLab studies, each data collection project should establish its own data monitoring protocol that connects these lab processes with study-specific details. This is also helpful to record the specific data monitoring actions performed because the lab-wide defaults might change over time.


## Setting Up
Once the central tracker data dictionary and a draft of the data monitoring protocol are prepared, the study lead should begin data monitoring by copying a set of scripts to the dataset.

From the [HPC shell](https://ndclab.github.io/wiki/docs/hpc/accessing.html), navigate to the datasets folder:
```
cd /home/data/NDClab/datasets
```

You will input a single command that indicates which dataset should be set up, which data types are involved, and which EEG system (if any) is used. Here is the core structure of the command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup.sh -t YOUR-DATASET/ DATA-TYPES SUBJECT-NUMBERING (-n)
```
* **-t FLAG:** always include this flag so that a tracker is generated on the basis of your central tracker data dictionary
* **YOUR-DATASET:** this is the name of your dataset
* **DATA-TYPES:** include each data type you have in your `sourcedata/raw/` folder, separated by a comma (no space); these must follow the conventions outlined in the datadict_definitions file (be sure to use either 'bv' or 'egi', rather than using 'eeg', so that the script knows which system was used to collect the data in the `sourcedata/raw/eeg/` folder)
* **SUBJECT-NUMBERING:** include the first subject number to be used
* **-n FLAG:** this optional flag allows you to specify if you only collected a single running EEG per participant, as opposed to one EEG file per PsychoPy task

Here is an example of the setup line for rwe-eeg-dataset. It includes five data types: audio, digi, eeg (for which we specify 'bv'), psychopy, and redcap. Subject numbering for the central tracker will begin at 210000. There was one EEG file per PsychoPy task, so the '-n' flag was not used.
```
bash /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup.sh -t rwe-eeg-dataset/ audio,digi,bv,psychopy,redcap 210000
```

Here is an second example of the setup line, this time for oops-faces-dataset. It includes four data types: digi, eeg (for which we specify 'bv'), psychopy, and redcap. Subject numbering for the central tracker will begin at 240001. There was only one running EEG file per participant (although there are two PsychoPy tasks), so the '-n' flag was used.
```
bash /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup.sh -t oops-faces-dataset/ digi,bv,psychopy,redcap 240001 -n
```

After executing this command, the following new files (in addition to the blank central tracker) will be added to your dataset's data-monitoring folder:
- hallMonitor.sh
- hallMonitor.sub
- preprocess.sub
- rename-cols.py
- check-id.py
- update-tracker.py

Details for each are available below.


## hallMonitor.sub

### Purpose
The hallMonitor script (hallMonitor.sh) is triggered by running the associated slurm file (hallMonitor.sub).  It checks that raw data (`sourcedata/raw`) is in good order and, once confirmed, places a copy of the data in `sourcedata/checked`. This serves two key purposes:
1. issues with the incoming data (e.g., improper file naming) are identified and corrected early.
2. downstream processes interact with the "checked" data and safeguard the integrity of the original "raw" data.

Specifically, hallMonitor performs the following checks:
#### REDCap
1. Identifies most recent REDCap CSV.
2. Copies this file to `sourcedata/checked/redcap`.
3. Updates all rows in the central tracker whose description begins "redcap_data:" by means of update-tracker.py.

#### Pavlovia/Psychopy
1. Checks for the existence of any new subject folders in `sourcedata/raw/pavlovia` or `sourcedata/raw/psychopy` and, if they are found, verifies the correct subject folder nomenclature (i.e., sub-XXXXXX).
2. For correctly-named, new subject folders, the folder is copied over to `sourcedata/checked/pavlovia` or `sourcedata/checked/psychopy`.
3. Checks folders in `sourcedata/raw/pavlovia` or `sourcedata/raw/psychopy`; if any new .csv files are found and these files match the task name as indicated in the central tracker data dictionary, the script checks that the subject ID within these files match the folder name, using check-id.py.  If successful, these files are copied to the existing subject folder in `sourcedata/checked.`
4. Verifies that there is only a single .csv file for each tracked task (that is, there are no duplicate records for a single participant). (If you have a situation where you do have two separate files, zipping one of them will prevent hallMonitor from throwing an error every time you run it.)
5. Updates all rows in the central tracker whose description begins "psychopy:" by means of update-tracker.py.

If any duplicate files or improper folder names are identified, hallMonitor outputs a red error message.

#### Zoom/Audio/Video/Digi
Audio, video, and photo (such as EEG digitization, "digi") files are managed manually by the study lead. Proper encryption should be verified (that is, decryption using the study password should be tested and confirmed), after which the participant's audio/video/digi files should be manually copied to `sourcedata/checked`.  The hallMonitor script simply verifies the existence of a folder in `sourcedata/checked` and updates the zoomData, audioData, videoData, and/or digiData columns of the central tracker accordingly (using update-tracker.py).

Within `sourcedata/checked`, folders should be organized as:<br/>
/checked/<br/>
├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
├── bidsish/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──digi/<br/>

#### EEG
1. Checks for the existence of any new subject folders in `sourcedata/raw/eeg` and, if they are found, verifies the correct subject folder nomenclature (i.e., sub-XXXXXX).
2. For correctly-named folders in `sourcedata/raw/eeg`:
    1. Verifies that file names within the folder match the subject ID of the folder itself.
    2. If the '-n' flag is used: verifies that there is only one of each file type, depending on the system used for data collection (BV (.eeg, .vhdr, .vmrk) or EGI (.mff)); any naming convention is acceptable. If the '-n' flag is not present: verifies that there is one of each expected file type for each PsychoPy task, with matching nomenclature.
    3. Verifies that file names follow the appropriate conventions for study subjects.

Any new folders, as well as new files within previously existing folders, that pass the above checks are copied to the existing subject folder in `sourcedata/checked/bidsish/sub-XXXXXX/eeg`.  The bvData or egiData row in the central tracker is updated accordingly (via update-tracker.py).

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
3. Arrow down to the last line, add a space after `./hallMonitor.sh`, then the flag (`-m` or `-r`) and the mapping or replacement details.
4. Save your changes by holding down the ctrl key and pressing the letter 'o'. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return.
5. To exit the nano view, hold down the ctrl key again and press the letter 'x'.

If you have added any modification to the REDCap header, this is executed (by running hallMonitor.sub) via the rename-cols.py script.

### How to Run
The hallMonitor script should be run weekly by the project lead. It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on fridays 'run hallMonitor'`).

To run the script, ensure that you are on the `main` branch of the repository on the HPC. Use `git pull` to update the HPC with any changes available on the GitHub remote.  Then follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

Review the output for errors requiring correction (by using `cat` to print the messages to the console). After making any necessary corrections, re-run the script until no errors are received, then remove all .out files to keep a tidy folder (`rm slurm-NUMBER.out`).

The hallMonitor script automatically updates the data-monitoring-log.md file in the dataset's data-monitoring folder.

Once you have completed the hallMonitor process and everything is tidy, push your changes back to the GitHub remote ([`git add`, `git commit`, `git push`](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html)).  This merely updates the data monitoring scripts, log, and central tracker on GitHub; it does not transfer any data from `sourcedata` nor `derivatives` (those only live on the HPC).


## `preprocess.sub`

### Purpose
Pre-processing scripts transform the data collected from participants (questionnaires, behavioral tasks) into aggregate numbers that can be used for data analysis. These should draw upon data in the `sourcedata/checked` folder and output to `derivatives/preprocessed`. The preprocess slurm script is a handy shortcut that binds together the automated scoring of REDCap data (via the instruments script) along with any other custom scripts that you tell it to run.

### Instruments
The preprocess slurm script calls the instruments scoring mechanism, which will identify the most recent REDCap file in `sourcedata/checked/redcap`, score it automatically, and output it to `derivatives/preprocessed`, having renamed the "DATA" in the original filename to "SCRD."  It also updates any rows in the central tracker whose description in the central tracker data dictionary begins with "redcap_scrd:".

### R/MATLAB/Python Scripts
You need to create and test these scripts first on local and individually on the HPC before binding them into preprocess.sub. This is very important because if you accidentally create an infinite loop on the HPC, you could burn through all of the lab's monthly time allottment on the HPC and you would be forced to do all your calculations by hand until the end of the month! :cold_sweat:

The wiki includes instructions for running standalone [R](https://ndclab.github.io/wiki/docs/hpc/r.html), [MATLAB](https://ndclab.github.io/wiki/docs/hpc/matlab.html), and [Python](https://ndclab.github.io/wiki/docs/hpc/python.html) scripts.

In addition to preprocessing your data, your R, MATLAB, or Python scripts must include the necessary code to update your study's central tracker when they run. Here is an example in R that can be modified for your script.  This example specifically updates the `readAloudDisfluencies_s1_r1_e1` variable in the central tracker if the subject ID has been included in the "disfluencySummaryDat" dataframe:
```
#load central tracker
track_path <- '/home/data/NDClab/datasets/readAloud-valence-dataset/data-monitoring/central-tracker_readAloud-valence-dataset.csv'
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
You must specify the container(s) and script(s) that you want included in the preprocess slurm script. Use the same `nano` command as above to modify the preprocess.sub file contents. Here is an example:
![preprocess-example](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/preprocess-example.png)

### How to Run
Pre-processing scripts should be created as early as possible in the data collection process (ideally to process even the first participant!), and then should be run by the project lead on a weekly basis to ensure that the incoming data appears to be in good order (for instance, we’re not seeing a trend of wild inaccuracy in simple computer tasks or strange numbers in questionnaire data). 

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

The preprocess slurm script automatically updates the data-monitoring-log.md file in the dataset's data-monitoring folder.

Once you have completed each run of preprocessing and everything is tidy, push your changes back to the GitHub remote ([`git add`, `git commit`, `git push`](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html)). This merely updates the data monitoring scripts, log, and central tracker on GitHub; it does not transfer any data from `sourcedata` nor `derivatives` (those only live on the HPC).


## Final Considerations
- If you switch to a new REDCap project during data collection (for instance, because you added a new instrument or corrected an old one), be sure to check any header mapping/replacements you added to `hallMonitor.sub` as these may need to be modified or deleted.
- When data collection is complete, you should comment out the lines in `preprocess.sub` that are no longer needed (for example, the lines that trigger the instruments script) so that you don't create unnecessary duplicates.