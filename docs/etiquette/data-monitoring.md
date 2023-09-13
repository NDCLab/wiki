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
5. [Setting Up](#setting-up)
6. [hallMonitor.sub](#hallmonitorsub)
7. [preprocess.sub](#preprocesssub)
8. [Protocol](#protocol)
9. [Final Considerations](#final-considerations)


## Overview
Data monitoring is an ongoing process during data collection and preprocessing. This process has three key goals:
1. Regularly check that data is in **good order** (e.g., proper organization and correct file naming).
2. Regularly check on data **quality** (e.g., preprocessed data points are not wildly different than expections, implying an error in the study experiment).
3. Maintain an up-to-date **central tracker** with all relevant data points per participant.

At this time, these steps are handled manually by study leads for data collection projects. The long-term goal of the NDCLab, however, is to automate these functions.


## Sourcedata Structure
Within `sourcedata/raw`, folders should be organized as follows (and as appropriate for the data being collected; not all folders will be required for all projects):<br/>
/raw/<br/>
├── s1_r1/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── redcap/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── psychopy/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├──sub-XXXXXX/<br/>

...and the same for `raw/s2_r1`, etc. Note that "audio" and "video" may be replaced with "audacity" and "zoom", respectively.


## Central Tracker
Each data collection project has a central tracker that provides a real-time overview of what data is available for each participant.


#### Data Dictionary
The rows and columns of the central tracker will be built directly from the contents of the `central-tracker_datadict.csv` file that you create.  The sample template includes instructions within [brackets] and text to edit within {curly brackets}.  Consult the `readme.md` file in `data-monitoring/data-dictionary/` for details on how to build the data dictionary.


#### Required Variables
The first column in every NDCLab central tracker is called "id" and it specifies the participant ID.
- The "allowedValues" section of the "id" row in the data dictionary should specify the IDs that are allowed for that given study, stated in integer notation with integer sets separated by commas (for example, a study with 5-digit IDs that start with the number 4 would state the allowedValues as "[40000,49999]"; a study with 7-digit IDs that either start with 200 or 201 would state the allowedValues as "[2000000,2009999],[2010000,2019999]")
- The setup script for data monitoring will populate the central tracker with IDs based on the ID variable found in a particular REDCap file. This is specified in the "description" section of the "id" row in the data dictionary (for example, the description could read "Participant ID (file: "thriveconsent"; variable: "record_id")" where the file and variable name are specified within double quotation marks). The only IDs that will populate in the central tracker are the IDs that exist in that REDCap file as the ID variable.

The second column in every NDCLab central tracker is called "consent" and it specifies whether the adult participant consented or not.
- The value of the consent column is based on the value of the "consent_complete" (or "consentes_complete") variable within REDCap data. Note that the consent instrument in REDCap must be named "consent" (or "consentes") in order for the "_complete" variable to be named properly.

If a study population includes participants under the age of 18, the third column in the central tracker will be called "assent" and it will specify whether the child participant assented or not.
- The value of the assent column is based on the value of the "assent_complete" variable within REDCap data. Note that the assent instrument in REDCap must be named "assent" in order for the "_complete" variable to be named properly.

Next, the central tracker will have columns related to non-questionnaire data (e.g., psychopy, audio/audacity, video/zoom, eeg, digi). 
- Each task within a given data type will have a column in the central tracker (based on the rows in the data dictionary for each task and data type intersection), and the columns will be named based on the variable name listed in the data dictionary with the appropriate suffix appended. The variable name in the data dictionary for non-questionnaire data should follow the convention of "`task` _ `dataType`" where `task` is the name of the task and `dataType` is the type of data collected during that task.
- Note: for instances in which a given data type's collection is not separated according to tasks (e.g., "`flanker` _ `eeg`" or "`social-interaction` _ `eeg`") but rather is collected across all tasks, the task name will be "all" (e.g., "`all` _ `eeg`").

For questionnaire data from REDCap, there will be one row in the data dictionary for each individual questionnaire, with the variable for that row named exactly as the questionnaire is. Thus, there will be one column in the central tracker for each quesionnaire, named exactly as the questionnaire is, with the appropriate suffix appended.

For scored data from REDCap questionnaires, there will be one row in the data dictionary for each individual subscore, with the variable for that row named exactly as the subscore is. Thus, there will be one column in the central tracker for each subscore, named exactly as the subscore is, with the appropriate suffix appended.

For custom variables, you will control these in your preprocessing scripts. In the data dictionary, be sure to specify how each is operating and include the name of the script in the provenance column.


#### File Name
Scripts in the data monitoring ecosystem access a study's central tracker based on its filename. For this reason, the nomenclature is standardized: `central-tracker_dataset-name`. For example, the `memory-for-error-dataset` project has a central tracker named `central-tracker_memory-for-error-dataset`. You do not need to name this file yourself, but you do need to ensure that the data dictionary you create for your central tracker is named `central-tracker_datadict.csv` and that it lives in `data-monitoring/data-dictionary/` within your dataset repository.


## Setting Up
Once the central tracker data dictionary is prepared, the study lead can begin data monitoring by copying a set of scripts to the dataset.

From the [HPC shell](https://ndclab.github.io/wiki/docs/hpc/accessing.html), navigate to the datasets folder:
```
cd /home/data/NDClab/datasets
```

You will input a single command that indicates which dataset should be set up, and the datatypes and other relevant information will be read from the central tracker data dictionary.

```
bash /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup.sh -t YOUR-DATASET
```
* **-t FLAG:** always include this flag so that a tracker is generated on the basis of your central tracker data dictionary, unless you have a preciously generated tracker.
* **YOUR-DATASET:** this is the name of your dataset

Here is an example of the setup line for rwe-eeg-dataset.
```
bash /home/data/NDClab/tools/lab-devOps/scripts/monitor/setup.sh -t rwe-eeg-dataset
```

After executing this command, the following new files (in addition to the blank central tracker) will be added to your dataset's data-monitoring folder:
- hallMonitor.sh
- hallMonitor.sub
- preprocess.sub
- rename-cols.py
- check-id.py
- update-tracker.py
- verify-copy.py

Details for hallMonitor and preprocess are available below.


## hallMonitor.sub

### Purpose
The hallMonitor script (hallMonitor.sh) is triggered by running the associated slurm file (hallMonitor.sub) while in `data-monitoring` (`cd your-dataset/data-monitoring`).  It checks that raw data (`sourcedata/raw`) is in good order and, once confirmed, places a copy of the data in `sourcedata/checked`. Errors in the names and structure of the files in `sourcedata/raw` are noted in the slurm-XXXX.out and slurm-XXXX_errorlog.out files. This serves two key purposes:
1. issues with the incoming data (e.g., improper file naming) are identified and corrected early.
2. downstream processes (like updating the central tracker) interact with the "checked" data and safeguard the integrity of the original "raw" data.

Specifically, hallMonitor performs the following checks:
#### REDCap
1. Identifies most recent uniquely named REDCap CSVs.
2. Copies these files to `sourcedata/checked/redcap`.
3. Updates all relevant rows in the central tracker by means of update-tracker.py.

#### Nonencrypted Data (Pavlovia/Psychopy, EEG, others)
1. Checks for the existence of new files in `sourcedata/raw/sX_rX/DATATYPE` and, if they are found, verifies the files are named correctly. Filenames follow the convention `sub-<NUMBER>_<task>_<dataType>_<suffix>.<extension>`, where NUMBER is the ID number, task is the name of the task (or "all" if data is collected across all tasks), dataType is the type of data, suffix is the session, run, and event the data was collected in (e.g., "s1_r1_e1"), and extension is the file's extension (e.g., ".csv").
2. For correctly-named files, files are copied over to `sourcedata/checked/sub-XXXXXX/sX_rX/DATATYPE`.
3. If any duplicate files or improper file or folder names are identified, hallMonitor outputs a red error message. This error message will be found in the slurm-XXXX.out and slurm-XXXX_errorlog.out files.

#### Encrypted Data (Audio/Video/Digi)
1. Audio, video, and photo (such as EEG digitization, "digi") files containing identifiable information are managed manually by the study lead. Proper encryption should be verified (that is, decryption using the study password should be tested and confirmed, see [here](https://ndclab.github.io/wiki/docs/technical-docs/data_encryption.html)), after which the participant's audio/video/digi files should be manually copied to `sourcedata/checked`. Filenames again follow the convention `sub-<NUMBER>_<task>_<dataType>_<suffix>.<extension>`.
2. The hallMonitor script simply verifies the existence and correct naming of the encyrpted (.gpg) files in `sourcedata/checked` and updates the audio/audacity, video/zoom, and/or digi columns of the central tracker accordingly (using update-tracker.py).
3. Incorrectly named files or folders are noted in an error message found in the slurm-XXXX.out and slurm-XXXX_errorlog.out files.

#### Checked Data Structure
Within `sourcedata/checked`, folders should be organized by subject, session, and datatype:<br/>
/checked/<br/>
├── redcap/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── sub-XXXXXX/<br/>
├── sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── s1_r1/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── psychopy/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── s2_r1/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── psychopy/<br/>
├── sub-XXXXXX/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── s1_r1/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── psychopy/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;├── s2_r1/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── eeg/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── digi/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── audio/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── video/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── psychopy/<br/>

...and the same for `/s3_r1/`, etc. Note that "audio" and "video" may be replaced with "audacity" and "zoom", respectively.

### Customize
Most customization required for the hallMonitor script is handled by the central tracker data dictionary. However, if REDCap column names need to be re-mapped to match the expectations of the instruments script, this can be built directly into hallMonitor. There are two options available:

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
3. Arrow down to the line calling hallMonitor, add a space after `./hallMonitor.sh`, then the flag (`-m` or `-r`) and the mapping or replacement details.
4. Save your changes by holding down the ctrl key and pressing the letter 'o'. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return.
5. To exit the nano view, hold down the ctrl key again and press the letter 'x'.

If you have added any modification to the REDCap header, this is executed (by running hallMonitor.sub) via the rename-cols.py script.

### How to Run
The hallMonitor script should be run weekly by the project lead. It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on fridays 'run hallMonitor'`).

To run the script, ensure that you are on the `main` branch of the repository on the HPC. Use `git pull` to update the HPC with any changes available on the GitHub remote.  Then follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

Review the error log output file for errors requiring correction (by using `cat` to print the messages to the console, i.e. `cat slurm-NUMBER_errorlog.out`). After making any necessary corrections, re-run the script until no errors are received, then remove all .out files to keep a tidy folder (`rm slurm-NUMBER.out`).

The hallMonitor script automatically updates the `data-monitoring-log.md` file in the dataset's data-monitoring folder with a description of the job's status and how many errors were encountered.

Once you have completed the hallMonitor process and everything is tidy, push your changes back to the GitHub remote ([`git add`, `git commit`, `git push`](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html)).  This merely updates the data monitoring scripts, log, and central tracker on GitHub; it does not transfer any data from `sourcedata` nor `derivatives` (those only live on the HPC).


## preprocess.sub

### Purpose
Pre-processing scripts transform the data collected from participants (questionnaires, behavioral tasks) into aggregate numbers that can be used for data analysis. These should draw upon data in the `sourcedata/checked` folder and output to `derivatives/preprocessed`. The preprocess slurm script is a handy shortcut that binds together the automated scoring of REDCap data (via the instruments script) along with any other custom scripts that you tell it to run.

### Instruments
The preprocess slurm script calls the instruments scoring mechanism, which will identify the most recent REDCap file in `sourcedata/checked/redcap`, score it automatically, and output it to `derivatives/preprocessed`, having renamed the "DATA" in the original filename to "SCRD."  It also updates any columns in the central tracker that are built from rows in the data dictionary that have the dataType "redcap_scrd".

### R/MATLAB/Python Scripts
You need to create and test these scripts first on local and individually on the HPC before binding them into preprocess.sub. This is very important because if you accidentally create an infinite loop on the HPC, you could burn through all of the lab's monthly time allottment on the HPC and you would be forced to do all your calculations by hand until the end of the month! :cold_sweat:

The wiki includes instructions for running standalone [R](https://ndclab.github.io/wiki/docs/hpc/r.html), [MATLAB](https://ndclab.github.io/wiki/docs/hpc/matlab.html), and [Python](https://ndclab.github.io/wiki/docs/hpc/python.html) scripts.

In addition to preprocessing your data, your R, MATLAB, or Python scripts must include the necessary code to update your study's central tracker when they run. Here is an example in R that can be modified for your script.  This example specifically updates the `readAloudDisfluencies_s1_r1_e1` variable in the central tracker if the participant ID has been included in the "disfluencySummaryDat" dataframe:
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
Pre-processing scripts should be created as early as possible in the data collection process (ideally to process even the first participant!), and then should be run by the project lead on a weekly basis to ensure that the incoming data appears to be in good order (for instance, ensuring we are not seeing a trend of wild inaccuracy in simple computer tasks or strange numbers in questionnaire data). 

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

The preprocess slurm script automatically updates the data-monitoring-log.md file in the dataset's data-monitoring folder.

Once you have completed each run of preprocessing and everything is tidy, push your changes back to the GitHub remote ([`git add`, `git commit`, `git push`](https://ndclab.github.io/wiki/docs/technical-docs/git_and_github.html)). This merely updates the data monitoring scripts, log, and central tracker on GitHub; it does not transfer any data from `sourcedata` nor `derivatives` (those only live on the HPC).


## Protocol
Although the broad strokes of data monitoring are identical across NDCLab studies, each data collection project should establish its own data monitoring protocol that connects these lab processes with study-specific details. Those study-specific details should be defined in the data collection project's dataset folder. The general template for the lab's data monitoring protocol is listed below.

### Data Uploads to the HPC
In order to run data monitoring scripts, data must first be uploaded to the HPC. The general guidelines for who uploads which data types and when is defined as:
- REDCap data is uploaded to `sourcedata/raw/sX_rX/redcap` by the study lead/coordinator twice a week (for ex: on Mondays and Thursdays). It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on mondays and thursdays 'upload REDCap data to HPC'`).
- All other data that is collected during a study visit (psychopy, eeg, digi, etc.) is uploaded by the RA(s) that conducted the visit as soon as the visit has concluded. Specific instructions regarding post-visit data backups are included in the project's study protocol.

### Decryption Checks
All encrypted data (audio,video, digi) that is uploaded to the HPC following a study visit must be checked for proper encryption within 3 days of upload. These decryption checks will be performed by assigned RAs who did not upload the data to the HPC, to ensure that the study decryption password works to decrypt the files. After checking for proper encryption, the RA will manually move the checked audio, video, and digi files to `sourcedata/checked`. Finally, the RA must update the study's decryption check log to indicate that the files passed the decryption check and were moved to `sourcedata/checked`.

The study lead/coordinator should perform weekly reviews to ensure that all encrypted data in `sourcedata/raw` has been checked for proper encryption and manually moved to `sourcedata/checked`.

### Running Data Monitoring
Data monitoring scripts (hallMonitor.sub and preprocess.sub) should be run once a week by the study lead/coordinator. It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on fridays 'run hallMonitor and preprocess'`).

After running hallMonitor, review the error log output file for errors requiring correction (by using `cat` to print the messages to the console, i.e. `cat slurm-NUMBER_errorlog.out`). You will need to make the necessary corrections so that errors are no longer received. There are two cases in which an error cannot or should not be directly corrected, but a note should be logged in the participant's folder to explain the lack of correction.

Case A: File name intentionally deviates from convention and does not require correction:
1. Ensure that the first portion of the file name leading up to the deviation matches file naming conventions and that the deviation is separated from the suffix by an underscore (refer to the "Intentional Deviations" section on the [Naming Conventions page](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html) for more details)
2. Add a text file named "corrected.txt" to the folder containing the uncorrected file. The "corrected.txt" file should contain an explanation for the file's intentional deviation from naming convention.
3. Manually move both the uncorrected file and the "corrected.txt" file to `sourcedata/checked`

Case B: Data was not collected for that participant:
1. Upon uploading data to the HPC following a study visit, the RA will make note of any data that was not collected by uploading blank text files called "no_\<datatype\>" (e.g., "no_digi") to the participant's folder.
2. Rename the "no_\<datatype\>" file to "corrected.txt", then edit the file to contain the text "This participant's data was not collected".
3. Manually move the "corrected.txt" file to `sourcedata/checked`

After making any necessary corrections, re-run the script until no errors are received. Ensure that `sourcedata/checked` and the central tracker have been updated to reflect the resolved errors, then remove all .out files to keep a tidy folder (`rm slurm-NUMBER.out`).


## Final Considerations
- If you switch to a new REDCap project during data collection (for instance, because you added a new instrument or corrected an old one), be sure to check any header mapping/replacements you added to `hallMonitor.sub` as these may need to be modified or deleted.
- When data collection is complete, you should comment out the lines in `preprocess.sub` that are no longer needed (for example, the lines that trigger the instruments script) so that you don't create unnecessary duplicates.
