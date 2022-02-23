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
2. [Usage](#usage)
3. [Adding New Instruments](#adding-new-instruments)


## Overview

The instruments repository is a collection of coding scripts that interpret a .json file and construct a unique survey object, which is then used to automatically score any input, as provided by the command line.

_For the less comp sci savvy_: the instruments script will automatically code the questionnaires that you have participants complete into the standard total scores and subscores.

## Usage

### Study Setup: Using an Existing Instrument

1. Clone the repository to your local machine.
2. Use the published PDF for submission to the FIU IRB.
3. Import the .zip to REDCap. Note that the .zip file uses `_s1_r1_e1`. These numerical values may need to be adjusted to meet the specific needs of your study's protocol; this requires changing the numerical values in the instrument name (within REDCap) and also the numerical values **in each variable**. No other change should be made to the variable names: other changes will break the link with the automated scoring script. See further details on the lab's [naming conventions for REDCap surveys](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap).
4. Save REDCap data to the HPC in accordance with your data collection protocol.

### Preprocessing Data

1. Log into the HPC [using the Visual Node](https://ndclab.github.io/wiki/docs/technical-docs/hpc-doc.html#connecting).  Launch Panther Shell Access:
![inst_open-shell](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/inst_open-shell.jpg)

2. You will be prompted to enter your password when the shell opens.  Type in your password and hit Enter.  The console will not show you that you are typing while inputting your password, but forge ahead!
![inst_input-password](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/inst_input-password.jpg)

3. Once you've logged into the HPC, navigate to the instruments repo located in the HPC by entering the following command:
    ```
    cd /home/data/NDClab/tools/instruments
    ```

4. We can use the script `process.sub` located in the `hpc/` folder to analyze data. First, we need to swap the string paths located below the comment that says "edit variables here to change inputs and outputs." You can edit files directly from the terminal by executing `nano hpc/process.sub`.

Example paths are in-place already. You will overwrite portions of each of the three lines:
    1. Replace "this-is-some-dataset" in the `project` variable to specify which project folder the data resides in. Examples of project folders are "rwe-dataset" or "memory-for-error-dataset."
    2. Replace "DATA" in the `input_file` variable to specify exactly which file should be processed.
    3. Replace "DATA" in the `output-file` variable to specify the file name you want for the processed version of the .csv.

    ```
    # edit variables here to change inputs and outputs
    project="this-is-some-dataset"
    input_file="/home/data/NDClab/datasets/$project/sourcedata/raw/DATA.csv"
    output_file="/home/data/NDClab/datasets/$project/derivatives/DATA.csv"
    ```

5. Lastly you can run this script by executing the command `sbatch hpc/process.sub`. This will output data to the `output_file` path that you've specified. Happy analyzing! 

## Adding New Instruments

1. Follow the lab's [GitHub etiquette](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html) to create a new branch off dev (`dev-NewInstrumentName`).
2. Create a new directory with the instrument's short name.
3. Add all of the following to the new directory: the published PDF, the REDCap PDF (shows exactly what participants see), and a REDCap import .zip that follows the lab's [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap). All REDCap import .zip files in the instruments repository should use `_s1_r1_e1`.
4. Add the (sub)score(s) for the instrument to the .json file with the appropriate parameters as described in subscore.py for subscale scoring.
5. Add the instrument, alphabeticaly, into the list-of-instruments.md with a link to the appropriate citation.
6. Push your branch to the remote, then open a PR and assign to the lab manager.
