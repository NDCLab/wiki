---
layout: default
title: Instruments
parent: Technical Documentation
nav_order: 4
---

![robots in  a factory](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/automation-header.jpg)  
*Basically what instruments does, but without the robot or the factory or the chips.*

Self-administered surveys are a popular method of research, and are used to measure certain metrics that pertain to participant emotional states or opinions. But, their excessive utility is often matched by their excessive tedium. Imagine you have 150 participants that filled multiple surveys on paper. This would involve scoring by-hand, a hardly interesting endeavor to take on while conducting research.

A solution would be to collect data via the internet and then apply code to automatically generate metrics. The NDClab's `instruments` repository aims to accomplish exactly that.

### Contents
1. [Overview](#overview)
    1. [Local Usage](#local-usage)  
    2. [HPC Usage](#hpc-usage)
2. [Development Guidelines](#development-guidelines)
    1. [Submit an issue](#submit-an-issue)  
    3. [Contribute to the code](#contribute-to-the-code)

## Overview

The instruments repository are a collection of coding scripts designed to interpret a json file and construct a unique survey object which will then be used to automatically score any input, as provided by the command line.

While its primary use is realized on the HPC, we can also work with this repository on our local machines. The details are listed below:

### Local Usage

To use instruments locally, we simply have to clone the repository and start up the docker container:

1. Clone the repository to your local machine, with `git clone` in your terminal. 
    ```
    git clone https://github.com/ndclab/instruments.git
    cd instruments
    ```

2. Build and activate a container using the OS-relevant files (see `containers/README.md`).

### HPC Usage

To use instruments in the NDClab' HPC folder, we can simply interact with the existing repository.

1. SSH into the computer cluster and navigate to the instruments repo located in the HPC.
    ```
    ssh userName@hpclogin01
    cd /home/data/NDClab/tools/instruments
    ```

2. We can use the script `process.sub` located in the `hpc/` folder to analyze data. All we have to do is swap the string paths located in the `input_file` variable and the `output_file` variable to match our intended inputs and outputs. If you are in a terminal, you can edit files directly from the terminal by executing `nano hpc/process.sub`.

    ```
    # load singularity module
    module load singularity-3.5.3

    # edit variables here to change inputs and outputs
    input_file="/home/data/NDClab/datasets/dataset1/sourcedata/raw/DATA.csv"
    output_file="/home/data/NDClab/datasets/dataset1/derivatives/DATA.csv"
    ```

3. Lastly you can run this script by executing the command `sbatch hpc/process.sub`. Happy analyzing! 

## Development Guidelines 

### Submit an issue
If you believe a new issue needs to be added to the [list of open issues](https://github.com/NDCLab/PEPPER-Pipeline/issues), feel free to create a new issue and select the appropriate template that suits the indicated change.

Once an issue has been created, the original author can likewise immediately assign themselves and start coding or documenting as described in [contribute to the code](#Contribute-to-the-Code). 

### Contribute to the Code
To get started on coding, follow the steps below. Note that you must have a GitHub account to collaborate on this project. All quoted commands are executed in your shell.

1. Fork the repo to your GitHub account by clicking on the "Fork" button on the top right corner of the [instruments repository](https://github.com/NDCLab/instruments):

2. Clone the repository to your local machine, with `git clone` in your terminal. Be sure to replace `user` below with your own GitHub username.
  ```
  git clone https://github.com/[user]/instruments.git
  cd instruments
  ```

3. Build and activate a container using the OS-relevant files (see `containers/README.md`).

4. Switch to the branch that you plan to contribute to. 

  * If work on this issue has already begun, then fetch and checkout the active branch and then create a sub-branch.
    ```
    git checkout dev-feature-issue
    git checkout -b dev-feature-issue-name
    ```

  * If this issue has not begun development, then create a new branch and then create a sub-branch.

    ```
    git checkout -b dev-feature-issue
    git checkout -b dev-feature-issue-name 
    ```

5. Implement changes (commit often!).

    ```
    git add file1 file2
    git commit -m "Attach flux capacitor" 
    ```

6. After you complete all your intended commits, push changes to branch.

    ```
    git push origin dev-feature-issue-name 
    ```