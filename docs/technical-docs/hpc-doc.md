---
layout: default
title: HPC Documentation
parent: Technical Documentation
nav_order: 1
---

![dt2-racks-from-front](https://user-images.githubusercontent.com/26397102/118044340-27148d00-b33c-11eb-8b2c-17a454f18c51.jpg)  
*Not the FIU HPC cluster*

## Outline 

* [Introduction](#Introduction)
* [Connecting to the HPC](#Connecting)
    * [Establishing VPN Connection](#VPN)
    * [Login Node](#Login-Node)
    * [Visual Node](#Visual-Node)
* [HPC File Structure](#Structure)
* [Singularity](#Singularity)
* [Slurm](#Slurm)
* [Jupyter](#Jupyter)  

## Introduction
The [FIU High-performance computing (HPC) cluster](http://ircc.fiu.edu/) is a group of interconnected computers designed to perform computationally "expensive" tasks. This includes processing large quantities of data and executing programs in parallel. 

While a personal computer with 6 cores could execute 6 programs in parallel, one of the 3000 compute nodes in the HPC cluster could execute 44 programs in parallel.

The following document details how to access and properly utilize this resource once an HPC account is granted. 

## Connecting
To use the HPC, a lab member must either use on-campus WiFi or utilize a VPN to access the [FIU intranet](https://en.wikipedia.org/wiki/Intranet). 

Once a secure connection is established, both the login node and visual node can be accessed for file manipulation and job submission. 

### VPN
If a lab member is using on-campus WiFi, this step can be safely skipped. 

However, if a lab member is accessing the HPC remotely, they must connect to the [FIU VPN](https://network.fiu.edu/vpn/). Link to point to VPN access here. 

### Login-Node

### Visual-Node

## Jupyter

1. Connect to the VPN. Launch the Panther desktop from the [HPC desktop](https://wwww.hpcgui.fiu.edu):

![launching-panther-desktop](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/hpc/launching-panther-desktop.png)


2. Once the desktop has launched, open the terminal. Load conda, then jupyter.

![terminal-actions-conda-jupyter](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/hpc/terminal-actions-conda-jupyter.png)
Note: we use a [conda environment](http://ircc.fiu.edu/custom-environments-and-package-installation-r-and-python/) for our scripts for version control. (We do not use pip.)

## Accessing the Private Queue on the HPC

1. Specify a slurm script.
    * Note private cue at top.
    * Always specify 'medium' and select one of the medium machines.

![jupyter-bash-specs](https://raw.githubusercontent.com/NDCLab/wiki/gh-pages/docs/_assets/hpc/jupyter-bash-specs.png)
