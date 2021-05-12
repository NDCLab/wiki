---
layout: default
title: HPC Documentation
parent: Technical Documentation
nav_order: 1
---

## Outline 

* [Introduction](#Introduction)
* [Connecting to HPC](#Connecting-to-HPC)
    * [VPN](#Establishing-VPN-connection)
    * [Login Node](#Login-Node)
    * [Visual Node](#Visual-Node)
* [HPC File Structure](#Structure)
* [Singularity](#Singularity)
* [Slurm](#Slurm)
* [Jupyter](#Jupyter)  

## Introduction
The [FIU High-performance computing (HPC) cluster](http://ircc.fiu.edu/) is a group of interconnected computers designed to perform computationally "expensive" tasks. This includes processing large quantities of data and executing programs in parallel. 

While a personal computer with 6 cores could execute 6 programs in parallel, one of the 3000 compute nodes in the HPC cluster could execute 44 programs in parallel.

The following doc details how to utilize this resource and points to other useful documentations.

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
