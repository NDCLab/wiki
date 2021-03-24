---
layout: default
title: HPC Documentation
parent: Technical Documentation
nav_order: 1
---

## Opening a Jupyter Notebook on the HPC

1. Connect to the VPN. Launch the Panther desktop from the [HPC desktop](https://wwww.hpcgui.fiu.edu):

![launching-panther-desktop](docs/_assets/hpc/launching-panther-desktop.png)


2. Once the desktop has launched, open the terminal. Load conda, then jupyter.

![terminal-actions-conda-jupyter](docs/_assets/hpc/terminal-actions-conda-jupyter.png)
Note: we use a [conda environment](http://ircc.fiu.edu/custom-environments-and-package-installation-r-and-python/) for our scripts for version control. (We do not use pip.)

## Accessing the Private Queue on the HPC

1. Specify a slurm script.
    * Note private cue at top.
    * Always specify 'medium' and select one of the medium machines.

![jupyter-bash-specs](docs/_assets/hpc/jupyter-bash-specs.png)
