---
layout: default
title: GitHub+HPC
parent: Study Setup
nav_order: 3
---

### Contents
1. [Overview](#overview)
2. [Data Types](#data-types)
3. [GitHub](#github)
4. [HPC](#hpc)
5. [Tips and Tricks](#tips-and-tricks)



## Overview
The lab manager creates a GitHub repository for each new data collection project in the lab. This repository is "mirrored" to the lab's HPC space, so that all materials and scripts that you make publicly available via GitHub are also available to you on the HPC. A nightly script runs a `git pull` to update the HPC with any new changes from the GitHub remote. If you have made modifications to the repository on the HPC, but you forgot to commit these changes and `git push` back to the Github remote, the nightly script may not be able to update because the two versions of the repository (the HPC version and the version on GitHub) are in conflict. In such cases, the project lead will receive an e-mail notification about the failure to sync, which should be quickly addressed.


## Data Types
Before any data is collected, it is imperative that you plan how data will be organized.  In particular, if you are adding a new type of data that is not already covered in the [Data Monitoring](https://ndclab.github.io/wiki/docs/etiquette/data-monitoring.html) section of the wiki, it will be important to cross-check that the lab’s existing processes, particularly those that protect personally-identifiable information, do not require modification to extend their protections to your incoming data.  (As an example, there are processes to ensure that personally-identifiable information is encrypted on the HPC.  If you will be collecting a new data format that the lab hasn’t used before, the lab technician will need to update the associated scripts.)


## GitHub
As you prepare a new study, all materials should be saved in the GitHub folder and regularly pushed to the remote repository.  This effectively acts as a back-up for all your work in case something happens to your computer.  By the time you begin data collection, the following should be clean and public-facing on GitHub:
- README.md
- CONTRIBUTING.md
- literature/
- materials/
     - Final versions of all task scripts (exception: PsychoPy tasks that will be run via Pavlovia should be on GitLab and GitHub should merely contain a message that GitLab repo will be made public at the end of data collection).
    - “Data Dictionary” export from REDCap showing the structure of all questionnaires
    - Pointer to the study protocol on gDrive
- data-monitoring/data-dictionary/
    - the default “datadict_definitions.csv”
    - the default csv file for each questionnaire included in REDCap, with "allowedSuffix" modified (as appropriate) to include any additional sessions/runs/events
    - a csv file for any study tasks (for example, with the output variables from PsychoPy/Pavlovia)
    - the initial central tracker data dictionary (see details [here](https://ndclab.github.io/wiki/docs/etiquette/data-monitoring.html#central-tracker)) 


## HPC
The only data that will exist on the HPC but not on the GitHub remote is the data within `sourcedata/` and `derivatives/`. These two folders are explicitly git-ignored. Any other changes you make directly to the project folder on the HPC (for example: modifying a script, setting up or running data monitoring activities, etc.) should be committed and pushed back (`git push`) to the GitHub remote in order to keep the HPC and the GitHub remote fully synced.


## Tips and Tricks
It is useful not to think of the GitHub remote, the project files on your local computer, and the project folder as separate locations. Instead, imagine them as a single universe that is available from three different points of entry. Your primary interactions should be on your local computer and on the HPC, with the GitHub remote serving as a waypoint between the two (with the awesome benefit of making the lab's work truly open science). Be sure to set yourself up to use Git on your [local computer](https://ndclab.github.io/wiki/docs/Onboarding/get-with-git.html) and on the [HPC](https://ndclab.github.io/wiki/docs/hpc/git-on-hpc.html), and then use a "pull-and-push" strategy to ensure you are always working with the most up-to-date version of your folder, regardless of where you log in.

