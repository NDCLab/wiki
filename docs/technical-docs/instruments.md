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
3. [Updating an Instrument](#updating-an-instrument)
4. [Some Technical Notes](#some-technical-notes)


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
3. Follow the instructions in the [study setup section](https://ndclab.github.io/wiki/docs/study-setup/redcap.html#adding-an-instrument) to load questionnaires into REDCap.
4. Save collected REDCap data in .csv format to the HPC in accordance with your data collection protocol.

### Preprocessing Collected Data
If you have already set up [data monitoring](https://ndclab.github.io/wiki/docs/etiquette/data-monitoring.html) for your study, the call for [`preprocess.sub`](https://ndclab.github.io/wiki/docs/etiquette/data-monitoring.html#preprocesssub) will actually call the instruments script automatically. If you have not yet completed setup of data monitoring for your study, you may also run a single REDCap .csv file through the script manually:

1. Notify the lab at large that you are working with the instruments repo by sending a message on the #tech channel on Slack. Only one person can run the script manually at a given time.

2. Log in to the [HPC](https://ndclab.github.io/wiki/docs/hpc/accessing.html) via the [shell](https://ndclab.github.io/wiki/docs/technical-docs/shell.html). You can do this via an `ssh` command on your local terminal or by accessing "Pather Shell Access" on the HPC webpage. 

3. Navigate to the instruments repo located on the HPC by entering the following command:
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

5. To save your changes to the .sub file, hold down the ctrl key and press the letter ‘o’. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return. Then, to exit the nano view, hold down the ctrl key again and press the letter ‘x’.

6. Lastly you can run this script by executing the command `sbatch hpc/process.sub`. This will output data to the `output_file` path that you've specified.

7. In order to keep the folder tidy, delete the .out file that is created.

8. Notify the lab on the #tech channel that you done with instruments so that someone else may use it.

9. The .csv file that is output is a replica of the input file (that is, all the original data points are still there), **plus** new columns that provide all (sub)scores for each questionnaire. Details on subscores are available in the data dictionary for each input questionnaire. Happy analyzing! 

## Adding New Instruments
Before building a new instrument, be certain that you have familiarized yourself with several other instruments commonly used by the lab before you build a new one, so that your newly created instrument will have a similar look and feel to existing questionnaires. Likewise, familiarize yourself with the structure of the `instruments` repository, in particular the readme files associated with each questionnaire.

### Building a New Instrument
In general, it is best to build new instruments in a "sandbox" project on REDCap, as opposed to a project that is intended for data collection. If you do not have access to a sandbox, talk to the lab manager for help.

1. In the Designer section on REDCap, under “Add new instrument,” select “Create a new instrument from scratch.”  REDCap will prompt you to select where the new instrument should be added to the current list of instruments in your project (but it doesn't make much difference as you can move it later).
2. Use the lab’s [standard naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap) to name the instrument.
3. Once the empty instrument is created, click to navigate into it and begin building out the questions. See below for some handy guidelines.
4. Most instruments should be [surveys](https://ndclab.github.io/wiki/docs/study-setup/redcap.html#surveys-and-the-survey-queue), which makes it possible to string them together into a survey queue for participants, and lets you add a pretty header.  Enable your new instrument as a survey and modify the survey settings to include the Survey Title and Survey Instructions (do not modify any of the other fields in the Survey Settings when creating a new default instrument for the lab).
5. Test your new instrument as a participant.  Make sure it looks professional. Give it both reasonable and unreasonable answers. Try leaving things blank. Once you’re certain it’s working perfectly, send a test to the lab manager, too, for a second pair of eyes.
6. When the new instrument is ready, click on “Choose Action” next to the instrument in the Designer view. Select “Download ZIP Instrument” and save the output file to your local computer and rename it “acronym_s1_r1_e1.zip.”
7. Output the PDF from REDCap, which shows the survey title and survey instructions, by clicking the PDF icon under “View PDF.”  Save the output file to your local computer and rename it “acronym_redcap-survey.pdf.”
8. Create the data dictionary for the instrument by following the examples available in other lab instruments. This will include one row for every question (exclude from the data dictionary any descriptive fields that do not house participant-collected data, since these fields do not output in data files).
9. If your new questionnaire will require scoring, identify the scoring mechanism (sum, average, etc.) and any (sub)scores that should be calculated. Add both the `scrd` (the score or subscore) and `perc` (the percentage complete for the score or subscore) variables to the data dictionary following [established lab conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap). Note that scoring mechanisms are often not totally evident from the questionnaire and/or paper, so it is imperative that you work carefully and then have someone (perhaps the lab manager) independently check your work. When in doubt, require all questions to be answered in order to output scores that are calculated by summing and require 80% of questions to be answered in order to output socres that are calculated by averaging.
10. Build out the readme file. In order to maintain consistency across lab instruments, find an instrument with similar specifications (e.g., similarity in versions or translation history) and use the readme for that instrument as your base to create the readme for your new instrument.

Please follow these guidelines when creating a new instrument for the lab:
* Be certain to follow the lab’s [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap) for variable names.  For initial creation, use “s1_r1_e1” because you will export this for other lab members to use.
* Use the same numerical values for choices as the source instrument.  This ensures that the output CSV for your new instrument is easy to score and aligns with other published uses of the questionnaire.
* Force all questions to be required unless there is a very good reason not to. In this way, all users know that the default is for all questions to be required, and they can adjust this as required by the IRB for their own study.
* Be careful which questions are marked as “Identifiers.”  In general (although there are exceptions), such questions should only appear in an “interest form” or "demographics" type instrument.
* Enable Survey Settings and include the appropriate Survey Title and Survey Instructions (you do not need to include the lab logo).
* Whenever appropriate, use a “Matrix of Fields” as these have a cleaner display for the participant.
* Take careful notes about the origin of questions, instructions, scoring criteria, and any translations. Include these in the readme (while making an effort to match the readme format of existing instruments).
* Where appropriate, use field embedding for a more professional appearance.
* Test your instrument thoroughly.
* Be aware that there is a multitude of online resources available for how to do cool things in REDCap, such as field embeddings, branching logic, data validation, and calculated fields, so go hunting for creative solutions to formatting hurdles!


### Adding to the Lab's "Instruments" Repository

1. Clone the repository to your local machine.
2. Follow the lab's [GitHub etiquette](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html#managing-a-project) to create a new branch off dev (`dev-NewInstrumentName`) and checkout this branch.
3. Create a new folder with the instrument's acronym.
4. Add all of the following to the new folder:
    * the published PDF (if available)
    * the PDF that you exported from REDCap ("acronym_redcap-survey.pdf")
    * the REDCap import .zip ("acronym_s1_r1_e1.zip")
    * the data dictionary CSV
    * the readme
5. Add the score(s) for the instrument to the .json file, in alphabetical order, with the appropriate parameters as described below. (Note that variations on an instrument, for example the 'parent' version or Spanish-language version, appear immediately after the 'main' version.)
6. Add the instrument, alphabeticaly, into the list-of-instruments.md with a link to the appropriate citation.
7. Commit your changes and push your branch to the remote, then initiate a pull request and assign to the lab manager for review.

### Scoring Instructions
The basic structure for each score is self-evident from the structure of surveys.json. The following three parameters are required:
* `questions`: item number of each question that should be used to calculate the score (if all questions should be included, use `null`)
* `score_type`: typically "sum" or "avg" (check subscore.py for other options)
* `threshold`: minimum percentage of response to calculate a score (typically 1.0 for "sum" and 0.8 for "avg")

Other common parameters include:
* `rev_questions`: item numbers for any questions that are included in the `questions` parameter and need to be reversed for scoring
* `answers`: (required if `rev_questions` is used) the possible response values

More rarely, you might need:
* `products`: useful if a score is calculated by combining some other set of scores (examples: ambirmbi, aq10); note that you can combine a set of questions with a set of products (example: spai) -- if you are using `products`, you must still include the `questions` parameter; include any questions that should be summed/averaged with the products, otherwise use `[]` to indicate that only the products should be manipulated
* `hide`: (required if `products` is used) specification of whether the set of scores used to calculate `products` should also be independently output to the scored file (`"hide": false`) or should not be output (`"hide": true`)

Finally, it is possible to create a custom scoring for complex surveys, such as the bpsqi.


### Including Sister Versions
In many cases, the lab has multiple "versions" of the same questionnaire for a different audience. Example include:
* child version of an adult questionnaire
* parent version of a child self report questionnaire
* Spanish-language version of an English questionnaire

All of these should be stored in the same folder of the instruments repository. In surveys.json, however, separate entries must be created for each. That is, `ders`, `dersp`, and `derspes` all live in the "ders" folder, but have three separate entries in surveys.json due to limitations in the ability of the script to parse instrument names.


### Creating Multiple Variations on a Questionnaire
Some instruments are NDCLab-specific and may need to exist in multiple variations. An example is the "initState" surveys, which ask pretask questions. The first of such instruments should have the "A" designation in its name (e.g., "initStateA"). To create subsequent versions:

1. Create a new instrument based on the instructions above.  The original instrument should already have an "A" in its name (e.g., postTaskA).  Replace this with "B" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the two questionnaires inside this repository into two subfolders.
3. Update the readme for the instrument to indicate what is special about this version.


## Updating an Instrument

An existing instrument should be updated when a new version is created (for example, a new post-task questionnaire) or when the discovery of an error means that an existing questionnaire must be corrected.

1. Create a new instrument based on the instructions above.  In so doing, use "_b" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the old questionnaire and the new one inside this repository into two subfolders (instrument_a and instrument_b). Note that we do not name the initial version with the "_a" marker by default, but we do add it to the folder name and readme once a "_b" version is released.
3. Make sure that your changes will not impact automatic scoring.  If you think they might (or you are not sure), ping the lab manager before proceeding.
4. Update the readme for the instrument to indicate the changes made and that the prior version is now deprecated.


## Some Technical Notes
The scoring script identifies an instrument name by the initial letter-string in the REDCap variable names. For example, the "ambirmbi" in `ambirmbi_s1_r1_e1`. It separately identifies the intersection of session/run/event in the REDCap variable names; in this case: 1/1/1. If you include the same survey twice in REDCap, such as `ambirmbi_s1_r1_e1` and `ambirmbi_s1_r1_e2`, the scoring script will output two sets of scores for you: one for the "e1" data and one for the "e2" data.

The script can also disambiguate between versions of a scorable instrument. If your survey includes `ambirmbi_b_s1_r1_e1`, the script will use the same scoring instructions as for any other set of "ambirmbi" variables. This means that new versions of the same survey ("ambirmbi," "ambirmbi_b," "ambirmbi_c") are all managed by a single "ambirmbi" section in surveys.json. Additionally, the script will keep these separate, so if you start data collection with `ambirmbi_s1_r1_e1` and subsequently add `ambirmbi_b_s1_r1_e1` to REDCap, you will get separate scores for each.

As part of the scoring process, the script calculates the percentage complete for each score. It does this by calculating how many responses (for a given participant, of course) exist in the set of questions needed to compute a particular score. If that percentage is below the scoring threshold defined in surveys.json for the score, it does not calculate the score. One happy side effect of this behavior is that you can hide or delete questions that you don't want participants to see without impacting the scoring behavior for the questions that remain.
