---
layout: default
title: PEPPER
parent: Technical Documentation
nav_order: 8
---

![baseeegheader](https://user-images.githubusercontent.com/26397102/117209976-b958e600-adbc-11eb-8f23-d6015a28935e.png)
*PEPPER in a nutshell*

### Contents

1. [Introduction](#Introduction)
2. [Pipeline Overview](#Pipeline-Overview)
    1. [Roadmap](#Roadmap)
    2. [Planning Documents](#Planning-Documents)
    3. [Features](#Features)
3. [Development Guidelines](#Development-Guidelines)
    1. [Submit an issue](#Submit-an-Issue)  
    2. [Create documentation](#Create-documentation)
    3. [Contribute to the code](#Contribute-to-the-code)
4. [Containers](#Containers)

## Introduction
Welcome to the PEPPER-Pipeline project! To get immediately started on collaborating, view [development guidelines](#Development-Guidelines). We welcome contributors from **all** backgrounds! 

The development of the PEPPER-Pipeline is focused on optimizing an automated, flexible, and easy-to-use preprocessing pipeline dedicated to EEG-preprocessing. 

Following the optimization of import and preprocessing tools, development will focus on building out a common core of EEG processing tools to handle ERP, time-frequency, and source-based analyses. To find out more about this, view [pipeline overview](#pipeline-overview).

## Pipeline Overview
The following section details the planning, motivation, and features behind the pepper pipeline. 

### RoadMap
To be implemented!

### Planning Docs
<img src="https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/outerloop.png" alt="UML Diagram for Outer-loop" width="400"/>

*UML diagram for run, which references to run:preprocess*

<img src="https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/preprocess.png" alt="UML Diagram for Preprocess" width="800"/>

*UML diagram for run:preprocess*

The UML diagrams above detail the discrete pipeline steps of the default `user_params.json` file: 

1. `load:data` (pipeline input)

    A subset of raw data described in `load_data` is extracted. 

2. `run:preprocess`

    The main script calls a series of functions, each one executing a step of the pipeline. Some functions simply utilize an existing MNE function while others are more involved. All, however, follow the same standard format: each feature always receives an EEG object and unpacked variables from the `params` dictionary in the main script. 

    Additionally, each pipeline step returns an EEG object and a dictionary describing the changes that occurred to that EEG object.
    
    Motivation behind each pipeline step is described in [features](#Features).

3. `write:output`

   At the very last step of the pipeline, each respective output is passed to a `write` module which transforms the summed outputs into a comprehensive file. 

Together, the contents of `user_params.json` and `output_preproc.json` define all details necessary to describe (such as in the methods and results section for a journal publication) the manipulations of the pre-processing pipeline and its outputs.

The long term goal is to automate the writing of these journal article sections via a script that takes "user_params.json" and "output_preproc.json" as inputs. In contrast, the output.log file reflects a much more verbose record of what was run, what the outputs were, and the presence of any warning/errors, etc.

### Features

#### 1-Filter

- High-pass filter the data using MNE functions
- Read in the "high pass" "low pass" fields from the `user_params.json` file to define filter parameters

#### 2-Reject Bad Channels

- Auto-detect and remove bad channels (those that are “noisy” for a majority of the recording)
- Write to output file (field "globalBad_chans") to indicate which channels were detected as bad

#### 3-Independent Component Analysis

  Overview: ICA requires a decent amount of [stationarity](https://towardsdatascience.com/stationarity-in-time-series-analysis-90c94f27322#:~:text=In%20t%20he%20most%20intuitive,not%20itself%20change%20over%20time.) in the data. This is often violated by raw EEG. One way around this is to first make a copy of the EEG data using automated methods to detect noisy portions of data and removing these sections. ICA is then run on the copied data after cleaning. The ICA weights produced by the copied dataset are copied back into original recording. In this way, we do not have to “throw out” sections of noisy data, while, at the same time, we are able to derive an improved ICA decomposition.

1. Prepica
    - Make a copy of the EED recording
    - For the copied data: high-pass filter at 1 Hz
    - For the copied data: segment by epoch  to “cut” the continuous EEG recording into arbitrary 1-second epochs
    - For the copied data: use automated methods (voltage outlier detection and spectral outlier detection) to detect epochs that are excessively “noisy” for any channel
    - For the copied data: reject (remove) the noisy periods of data
    - Write to the output file which segments were rejected and based on what metrics
2. ICA
    - Run ICA on the copied data
    - Copy the ICA weights from the copied data back to the pre-copy data
3. Rejica
    - Use automated methods (TBD) to identify ICA components that reflect artifacts
    - Remove the data corresponding to the identified artifacts
    - Write to the output file (field "icArtifacts") which ICA components were identified as artifacts

#### 4-Segment
- Segment by epoch to "cut" the continuous data into epochs of data such that the zero point for each epoch is a given marker of interest
- Write to output file (field "XXX") which markers were used for epoching purposes, how many of each epoch were created, and how many milliseconds were retained before/after the markers of interest

#### 5-Final Reject Epochs
- Loop through each channel. For a given channel, loop over all epochs for that channel and identify epochs for which that channel, for a given epoch, exceeds either the voltage threshold or spectral threshold. If it exceeds the threshold, reject the channel data for this channel/epoch.
- Write to the output file ("field XXX") which channel/epoch intersections were rejected

#### 6-Interpolate
- Interpolate missing channels, at the channel/epoch level, using a spherical spline interpolation, as implemented in MNE
- Interpolate missing channels, at the global level, using a spherical spline interpolation, as implemented in MNE
- Write to output file (field "XXX") which channels were interpolated and using what method

#### 7-Re-reference
- Re-reference the data to the average of all electrodes (“average reference”) using the MNE function
- Write to output file (field "XXX") which data were re-referenced to average


## Development Guidelines

### Submit an Issue
If you believe a new issue needs to be added to the [list of open issues](https://github.com/NDCLab/PEPPER-Pipeline/issues):
* Verify that the suggestion does not already exist 
* Use the appropriate issue template

### Create Documentation
If you believe documentation needs to be added for a feature, test, or anything else create an issue and use the "Documentation request" issue template. 

<img width="731" alt="Untitled" src="https://user-images.githubusercontent.com/26397102/135634174-4c0be5fa-88d2-4377-9e2e-4e3f8ff0e5da.png">


### Contribute to the Code
If someone is already assigned to an issue that you intend to work on, post a comment to ask if you can help before assigning yourself.

If you do not receive a response within **24 hours**, then you are free to start work on the issue, but be sure to loop them in on your development plans. 

To get started on coding, follow the listed steps below. Note that you must have a GitHub account to collaborate to this project. All quoted commands are executed in your shell.

1. Fork the repo to your GitHub account by clicking on the "Fork" button on the top right corner of the [PEPPER repository](https://github.com/NDCLab/pepper-pipeline):
<img width="950" alt="Untitled" src="https://user-images.githubusercontent.com/26397102/135622318-46cd9a5a-06e6-47eb-9afc-0f0a56655b3e.png">

2. Clone the repository to your local machine, with `git clone` in your terminal. Be sure to replace `user` below with your own GitHub username.
  ```
  git clone https://github.com/[user]/pepper-pipeline.git
  cd pepper-pipeline/
  ```

3. Build and activate a container using the OS relevant files (see `container/README.md`).

4. Switch to the branch that you plan to contribute to. 

  * If work on this issue has already begun, then fetch and checkout the active branch.
    ```
    git fetch
    git checkout dev-feature-issue
    ```

  * If this issue has not begun development, then create a new branch.

    ```
    git checkout -b dev-feature-issue 
    ```

5. Create a sub-branch using your name/identifier. 

    ```
    git checkout dev-feature-issue-name 
    ```

6. Implement changes (commit often!).

    ```
    git add file1 file2
    git commit -m "Attached flux capacitor" 
    ```

7. After you complete all your intended commits, push changes to branch.

    ```
    git push 
    ```

8. Create a pull-request using the GitHub GUI. 

## Containers
Please use the dockerfile & singularity recipe located in `container/`. Directions on installation and usage are located in `container/README.md`. 