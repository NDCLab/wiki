---
layout: default
title: Instruments
parent: Technical Documentation
nav_order: 4
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
    3. Check the output_file path. This should typically just be "derivatives/preprocessed/".

        ```
        # edit variables here to change inputs and outputs
        project="this-is-some-dataset"
        input_file="/home/data/NDClab/datasets/$project/sourcedata/raw/DATA.csv"
        output_file="/home/data/NDClab/datasets/$project/derivatives/preprocessed/
        ```

5. To save your changes to the .sub file, hold down the ctrl key and pressing the letter ‘o’. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return. Then, to exit the nano view, hold down the ctrl key again and press the letter ‘x’.
6. Lastly you can run this script by executing the command `sbatch hpc/process.sub`. This will output data to the `output_file` path that you've specified.
7. The .csv file that is output is a replica of the input file (that is, all the original data points are still there), **plus** new columns that provide all (sub)scores for each questionnaire. Details on subscores are available in the data dictionary for each input questionnaire. Happy analyzing! 

## Adding New Instruments

1. Follow the lab's [GitHub etiquette](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html) to create a new branch off dev (`dev-NewInstrumentName`).
2. Create a new directory with the instrument's short name.
3. Add all of the following to the new directory:
    * the published PDF
    * the REDCap PDF (shows exactly what participants see)
    * a REDCap import .zip that follows the lab's [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap) – all REDCap import .zip files in the instruments repository should use `_s1_r1_e1` and should have Survey Settings enabled with the appropriate Survey Title and Survey Instructions added
    * a data dictionary CSV
4. Add the (sub)score(s) for the instrument to the .json file with the appropriate parameters as described in subscore.py for subscale scoring.
5. Add the instrument, alphabeticaly, into the list-of-instruments.md with a link to the appropriate citation.
6. Push your branch to the remote, then open a PR and assign to the lab manager.

## Updating Instruments

Instruments should be updated when a new version of a questionnaire is created or when the discovery of an error means that a questionnaire must be corrected.

### When the New Questionnaire Will Supersede the Old
1. Create a new instrument based on the instructions above.  In so doing, use "_b" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the old questionnaire and the new one inside this repository into two subfolders (instrument_a and instrument_b).
3. Make sure that your changes will not impact automatic scoring.  If you think they might (or you are not sure), ping the lab manager before proceeding.
4. Update the readme for the instrument to indicate the changes made and that the prior version is now deprecated.

### When the Lab Will Use Multiple Variations on a Questionnaire
1. Create a new instrument based on the instructions above.  The original instrument should already have an "A" in its name (e.g., postTaskA).  Replace this with "B" (or whichever is the next letter in the alphabet) within the instrument name and all variables.
2. Separate the two questionnaires inside this repository into two subfolders.
3. Update the readme for the instrument to indicate what is special about this version.
