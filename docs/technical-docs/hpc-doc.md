---
layout: default
title: HPC Documentation
parent: Technical Documentation
nav_order: 1
---

## Jupyter Notebook on the HPC

1. Launch the Panther desktop from the [HPC desktop](https://wwww.hpcgui.fiu.edu)
![launching-panther-desktop](https://github.com/NDCLab/wiki/tree/gh-pages/docs/_assets/hpc/launching-panther-desktop.png)

2. Once the desktop has launched, open the terminal. Load conda, then jupyter.
![terminal-actions-conda-jupyter](https://github.com/NDCLab/wiki/tree/gh-pages/docs/_assets/hpc/terminal-actions-conda-jupyter)
We use a [conda environment](http://ircc.fiu.edu/custom-environments-and-package-installation-r-and-python/) for our scripts for version control. (We do not use pip.)

3. Specify a slurm script.
    * Note private cue at top.
    * Always specify 'medium' and select one of the medium machines.
![jupyter-bash-specs](https://github.com/NDCLab/wiki/tree/gh-pages/docs/_assets/hpc/jupyter-bash-specs)