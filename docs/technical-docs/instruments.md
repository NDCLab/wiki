---
layout: default
title: Instruments
parent: Technical Documentation
nav_order: 5
---

![robots in a factory](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/inst_automation-header.jpg)  
*Basically what instruments does, but without the robot or the factory or the chips.*

Self-administered surveys are a popular method of research, and are used to measure certain metrics that pertain to participant emotional states or opinions. But their excessive utility is often matched by their excessive analytical tedium. Imagine you have 150 participants that filled multiple surveys on paper. This would involve scoring by hand, a hardly interesting endeavor to take on while conducting research.

A solution would be to collect data via the internet and then apply code to automatically generate metrics. The `instruments` repository aims to accomplish exactly that.

### Contents
1. [Overview](#overview)
2. [Using Existing Instruments](#using-existing-instruments)
3. [Adding New Instruments](#adding-new-instruments)
3. [Updating Instruments](#updating-instruments)


## Overview

The instruments repository is a collection of structured questionnaires and coding scripts. It includes, for each questionnaire:
* a .zip that can be uploaded directly into REDCap
* a .pdf that can be submitted to the IRB
* a .csv data dictionary
* code to convert raw data into scored data
* a readme with useful information and citation information

The coding scripts interpret a .json file and construct a unique survey object, which is then used to automatically score any input, as provided by the command line. _For the less comp sci savvy_: the instruments script will automatically code the questionnaires that you have participants complete into the standard total scores and subscores.

## Using Existing Instruments

### Study Setup

1. Clone the repository to your local machine. (Stay on the `main` branch.)
2. Use the PDF for submission to the FIU IRB.
3. Import the .zip to REDCap.
4. If you will use the same questionnaire more than once (e.g., asking the participant before and after completing a task), you will need to adjust the `_s1_r1_e1` parameters for both the instrument name and for each variable inside REDCap. Ensure that duplicate instruments match the `_s1_r1_e1` instrument exactly, but for the session/run/event numbers. No other change should be made to the variable names: other changes will break the link with the automated scoring script. See further details on the lab's [naming conventions for REDCap surveys](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap).
5. Save collected REDCap data in .csv format to the HPC in accordance with your data collection protocol.

### Preprocessing Collected Data

1. Log into the HPC [using the Visual Node](https://ndclab.github.io/wiki/docs/technical-docs/hpc-doc.html#connecting).  Launch Panther Shell Access:
![inst_open-shell](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/inst_open-shell.png)

2. You will be prompted to enter your password when the shell opens.  Type in your password and hit Enter.  The console will not show you that you are typing while inputting your password, but forge ahead!
![inst_input-password](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/inst_input-password.png)

3. Once you've logged into the HPC, navigate to the instruments repo located in the HPC by entering the following command:
    ```
    cd /home/data/NDClab/tools/instruments
    ```

4. We can use the script `process.sub` located in the `hpc/` folder to analyze data. First, we need to swap the string paths located below the comment that says "edit variables here to change inputs and outputs." You can edit files directly from the terminal by executing `nano hpc/process.sub`.  This opens the .sub file within your shell so that you can modify its contents.

    Example paths are in-place already. You will overwrite portions of each of the three lines:

    1. Replace "this-is-some-dataset" in the `project` variable to specify which project folder the data resides in. Examples of project folders are "rwe-dataset" or "memory-for-error-dataset."
    2. Replace "DATA" in the `input_file` variable to specify exactly which file should be processed.
    3. Check the output_file path. This should typically remain unchanged ("../derivatives/preprocessed/").

        ```
        # edit variables here to change inputs and check output path
        project="this-is-some-dataset"
        input_file="/home/data/NDClab/datasets/$project/sourcedata/raw/DATA.csv"
        output_file="/home/data/NDClab/datasets/$project/derivatives/preprocessed/"
        ```

5. To save your changes to the .sub file, hold down the ctrl key and pressing the letter ‘o’. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return. Then, to exit the nano view, hold down the ctrl key again and press the letter ‘x’.
6. Lastly you can run this script by executing the command `sbatch hpc/process.sub`. This will output data to the `output_file` path that you've specified.
7. The .csv file that is output is a replica of the input file (that is, all the original data points are still there), **plus** new columns that provide all (sub)scores for each questionnaire. Details on subscores are available in the data dictionary for each input questionnaire. Happy analyzing! 

## Adding New Instruments
Before building a new instrument, be certain that you have familiarized yourself with several other instruments commonly used by the lab before you build a new one, so that your newly created instrument will have a similar look and feel to existing questionnaires. Likewise, familiarize yourself with the structure of the `instruments` repository, in particular the readme files associated with each questionnaire.

### Building a New Instrument
In general, it is best to build new instruments in a "sandbox" project on REDCap, as opposed to a project that is intended for data collection. If you do not have access to a sandbox, talk to the lab manager for help.

1. In the Designer section on REDCap, under “Add new instrument,” select “Create a new instrument from scratch.”  REDCap will prompt you to select where the new instrument should be added to the current list of instruments in your project (but it doesn't make much difference as you can move it later).
2. Use the lab’s [standard naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap) to name the instrument.
3. Once the empty instrument is created, click to navigate into it and begin building out the questions. See below for some handy guidelines.
4. Most instruments should be [surveys](https://ndclab.github.io/wiki/docs/study-setup/redcap.html#surveys-and-the-survey-queue), which makes it possible to string them together into a survey queue for participants, and lets you add a pretty header.  Enable your new instrument as a survey and modify the survey settings to include the Survey Title and Survey Instructions (do not modify any of the other fields in the Survey Settings when creating a new default instrument for the lab).
5. Test your new instrument as a participant.  Make sure it looks professional. Give it both reasonable and unreasonable answers. Try leaving things blank. Once you’re certain it’s working perfectly, send a test to the lab manager, too, for a second pair of eyes.
6. When the new instrument is ready, click on “Choose Action” next to the instrument in the Designer view. Select “Download ZIP Instrument” and save the output file to your local computer and rename it “acronym_s1_r1_e1.zip”.
7. Output the PDF from REDCap, which shows the survey title and survey instructions, by clicking the PDF icon under “View PDF.”  Save the output file to your local computer and reename it “acronym_redcap-survey.pdf”.
8. Create the data dictionary for the instrument by following the examples available in other lab instruments. This will include one row for every question (exclude from the data dictionary any descriptive fields that do not house participant-collected data, since these fields do not output in data files).
9. If your new questionnaire will require scoring, identify the scoring mechanism (sum, average, etc.) and any (sub)scores that should be calculated. Add both the `scrd` (the score or subscore) and `perc` (the percentage complete for the score or subscore) variables to the data dictionary following [established lab conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap). Note that scoring mechanisms are often not totally evident from the questionnaire and/or paper, so it is imperative that you work carefully and then have someone (perhaps the lab manager) independently check your work. When in doubt, require all questions to be answered in order to output scores that are calculated by summing and require 80% of questions to be answered in order to output socres that are calculated by averaging.
10. Build out the readme file. In order to maintain consistency across lab instruments, find an instrument with similar specifications (e.g., similarity in versions or translation history) and use the readme for that instrument as your base to create the readme for your new instrument.

Please follow these guidelines when creating a new instrument for the lab:
* Be certain to follow the lab’s [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap) for variable names.  For initial creation, use “s1_r1_e1” because you will export this for other lab members to use.
* Use the same numerical values for choices as the source instrument.  This ensures that the output CSV for your new instrument is easy to score and aligns with other published uses of the questionnaire.
* Force all questions to be required unless there is a good reason not to (for example, for potentially sensitive questions where the IRB protocol indicates that participants will have the choice on whether or not to answer).
* Be careful which questions are marked as “Identifiers.”  In general (although there are exceptions), such questions should only appear in an “interest form” type instrument.
* Enable Survey Settings and include the appropriate Survey Title and Survey Instructions (you do not need to include the lab logo).
* Whenever appropriate, use a “Matrix of Fields” as these have a cleaner display for the participant.
* Take careful notes about the origin of questions, instructions, scoring criteria, and any translations. Include these in the readme (while making an effort to match the readme format of existing instruments).
* Where appropriate, use field embedding for a more professional appearance.
* Test your instrument thoroughly.
* Be aware that there is a multitude of online resources available for how to do cool things in REDCap, such as field embeddings, branching logic, data validation, and calculated fields, so go hunting for creative solutions to formatting hurdles!


### Adding to the Lab's "Instruments" Repository

1. Follow the lab's [GitHub etiquette](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html) to create a new branch off dev (`dev-NewInstrumentName`) and checkout this branch.
2. Create a new folder with the instrument's acronym.
3. Add all of the following to the new folder:
    * the published PDF (if available)
    * the PDF that you exported from REDCap ("acronym_redcap-survey.pdf")
    * the REDCap import .zip ("acronym_s1_r1_e1.zip")
    * the data dictionary CSV
    * the readme
4. Add the score(s) for the instrument to the .json file with the appropriate parameters as described in subscore.py for subscale scoring.
5. Add the instrument, alphabeticaly, into the list-of-instruments.md with a link to the appropriate citation.
6. Commit your changes and push your branch to the remote, then initiate a pull request and assign to the lab manager for review.


## Updating Instruments

Instruments should be updated when a new version of a questionnaire is created or when the discovery of an error means that a questionnaire must be corrected.

1. Create a new instrument based on the instructions above.  In so doing, use "_b" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the old questionnaire and the new one inside this repository into two subfolders (instrument_a and instrument_b). Note that we do not name the initial version with the "_a" marker by default, but we do add it to the folder name and readme once a "_b" version is released.
3. Make sure that your changes will not impact automatic scoring.  If you think they might (or you are not sure), ping the lab manager before proceeding.
4. Update the readme for the instrument to indicate the changes made and that the prior version is now deprecated.

## Multiple Variations on a Questionnaire

Some instruments are designed within the lab and may need to exist in multiple variations. An example is the "initState" surveys, which ask pretask questions. The first of such instruments should have the "A" designation in its name (e.g., "initStateA"). To create subsequent versions:

1. Create a new instrument based on the instructions above.  The original instrument should already have an "A" in its name (e.g., postTaskA).  Replace this with "B" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the two questionnaires inside this repository into two subfolders.
3. Update the readme for the instrument to indicate what is special about this version.
