---
layout: default
title: Instruments
parent: Technical Documentation
nav_order: 4
---

![robots in  a factory](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/automation-header.jpg)  
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

1. SSH into the computer cluster and navigate to the instruments repo located in the HPC.
  ```
  ssh userName@hpclogin01
  cd /home/data/NDClab/tools/instruments
  ```

2. While instruments is set up to automatically run over data-files, we can use example scripts located in the `hpc/` folder.

## Adding New Instruments

1. Follow the lab's [GitHub etiquette](https://ndclab.github.io/wiki/docs/etiquette/github-etiquette.html) to create a new branch off dev (`dev-NewInstrumentName`).
2. Create a new directory with the instrument's short name.
3. Add all of the following to the new directory: the published PDF, the REDCap PDF (shows exactly what participants see), and a REDCap import .zip that follows the lab's [naming conventions](https://ndclab.github.io/wiki/docs/etiquette/naming-conventions.html#redcap). All REDCap import .zip files in the instruments repository should use `_s1_r1_e1`.
4. Add the (sub)score(s) for the instrument to the .json file with the appropriate parameters as described in subscore.py for subscale scoring.
5. Add the instrument, alphabeticaly, into the list-of-instruments.md with a link to the appropriate citation.
6. Push your branch to the remote, then open a PR and assign to the lab manager.
