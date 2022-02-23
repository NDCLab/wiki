---
layout: default
title: Instruments
parent: Technical Documentation
nav_order: 4
---

![automation-header](https://user-images.githubusercontent.com/26397102/154751422-abacadda-f888-45f7-975a-bd41ad4c96b5.jpg)
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

1. Log into the FIU computer cluster through the [FIU HPC GUI](https://hpcgui.fiu.edu/). Once accessed, enter the terminal by clicking on the **Clusters** tab and then **Panther Shell Access** in the dropdown menu.

&nbsp;&nbsp;<img width="800" alt="step1_shell" src="https://user-images.githubusercontent.com/26397102/155373543-f7cbfdfc-4db7-48cd-9cf5-0f80bc83e520.png">

2. This will prompt you for your FIU password. Text will not appear on your terminal for privacy as you type in your password and you will have to hit the "enter" key to input your password. A screen containing this text should greet you if you have entered your password correctly:

    ```
    - Purge Policy - 
    The shared file systems - /home and /scratch - should not be used for long term storage. 
    Files in these locations are not backed up or guaranteed by IRCC. 
    In the event of a file system crash or purge, these files cannot be recovered. 
    It is the user's responsibility to back up all important data elsewhere.
    Files located in the /scratch space are automatically removed after 30 days.
    - Questions and Problem Reports -
            --> UTS Helpdesk:       http://utshelp.fiu.edu
            --> IRCC website:       http://ircc.fiu.edu
            --> QuickStart Guide:   http://ircc.fiu.edu/download/user-guides/Panther_Cluster_QuickStart_Guide.pdf
    -----------------------------------------------------------------------
    Note: You may run the "myquota" command to check your "home" disk quota.
    #######################################################################
    *******************************************************************************
    *                                                                             *
    *              AUTHORIZED PERSONNEL ONLY                                      *
    *                                                                             *
    *  If you are not legitimately authorized to use this server,                 *
    *  you must log out immediately and not reconnect. Please contact your        *
    *  supervisor for proper authorization.                                       *
    *                                                                             *
    *           Unauthorized use will be prosecuted.                              *
    *                                                                             *
    *******************************************************************************
    ```
    
3. Once you've logged into the HPC, navigate to the instruments repo located in the HPC by entering the following command:
    ```
    cd /home/data/NDClab/tools/instruments
    ```

4. We can use the script `process.sub` located in the `hpc/` folder to analyze data. All we have to do is swap the string paths located below the comment that says "edit variables here to change inputs and outputs." You can edit files directly from the terminal by executing `nano hpc/process.sub`.

Example paths are in-place already. We have to replace the "project" variable to specify which project the data resides in, the "input_file" variable to specify which file we are preprocessing, and lastly the "output_file" to specify where the data is written.

    ```
    # edit variables here to change inputs and outputs
    project="readAloud-valence-dataset"
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
