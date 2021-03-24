---
layout: default
title: HPC Documentation
parent: Technical Documentation
nav_order: 1
---

## Jupyter Notebook on the HPC

1. Launch the Panther desktop from the [HPC desktop](https://wwww.hpcgui.fiu.edu):
   (note: the HPC desktop cannot be accessed until you connect to the VPN)

![launching-panther-desktop](https://github.com/NDCLab/wiki/blob/cb92be615224b3ade40ea379426ca8c763ee90e5/docs/_assets/hpc/launching-panther-desktop.png)


2. Once the desktop has launched, open the terminal. Load conda, then jupyter.

![terminal-actions-conda-jupyter](https://github.com/NDCLab/wiki/blob/cb92be615224b3ade40ea379426ca8c763ee90e5/docs/_assets/hpc/launching-panther-desktop.png)
Note: we use a [conda environment](http://ircc.fiu.edu/custom-environments-and-package-installation-r-and-python/) for our scripts for version control. (We do not use pip.)

## Accessing the private queue on the HPC

1. Specify a slurm script.
    * Note private cue at top.
    * Always specify 'medium' and select one of the medium machines.

![jupyter-bash-specs](https://github.com/NDCLab/wiki/blob/68cf76de04cb86644ad19718504d9296d89c9385/docs/_assets/hpc/terminal-actions-conda-jupyter.png)
