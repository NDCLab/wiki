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
4. [hallMonitor.sub](#hallmonitor.sub)
5. [preprocess.sub](#preprocess.sub)



## Overview
Purpose of data monitoring and big picture of what it entails.
Everything machine readable
Eventually automated.



## Central Tracker
instructions on how to set up a central tracker
must pre-populate subject ids


## Protocol
instructions for setting up a protocol with study-specific details


## hallMonitor.sub

### Purpose
The hallMonitor script checks that raw data (`sourcedata/raw`) is in good order and, once confirmed, places a copy of the data in `sourcedata/checked`. This serves two key purposes:
1. issues with the incoming data (e.g., improper file naming) are identified and corrected early
2. downstream processes interact with the "checked" data and safeguard the integrity of the original "raw" data

### Customize
instructions on how to customize this on a per-project basis

### How to Run
The hallMonitor script should be run weekly by the project lead. It is recommended that you create a recurring reminder on your calendar or on Slack (`/remind me on fridays 'run hallMonitor'`).

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

Review the output for errors requiring correction. After making any necessary corrections, re-run the script until no errors are received, then remove all .out files to keep a tidy folder (`rm slurm-NUMBER.out`).


## preprocess.sub

### Purpose
Pre-processing scripts transform the data collected from participants (questionnaires, behavioral tasks) into aggregate numbers that can be used for data analysis. 
(checked>derivatives/preprocessed)

### Instruments
explanation of connection to instruments, pointer to wiki page

### R/MATLAB scripts
(need to create and test these scripts first on local and on hpc, incl pointer to RStudio/MATLAB HPC pages)
important because you could burn all our time on hpc if you create an infinite loop, calculations by hand until the end of the month!

### Customize
instructions on how to customize the .sub to combine preprocessing scripts on a per-project basis

### How to Run
Pre-processing scripts should be created as early as possible in the data collection process (ideally to process even the first participant!), and then should be run by the project lead on a weekly basis to ensure that the incoming data appears to be in good order (for instance, we’re not seeing a trend of wild inaccuracy in simple computer tasks or strange numbers in questionnaire data). 

To run the script, follow the instructions [here](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).
