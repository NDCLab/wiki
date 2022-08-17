---
layout: default
title: Matlab
parent: HPC
nav_order: 6
---

### Contents
1. [Packages](#packages)
2. [Running a MATLAB Script](#running-a-matlab-script)
3. [MATLAB GUI](#matlab-gui)


## Packages


## Running a MATLAB Script
To run a script in the MATLAB programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
sh /home/data/NDClab/tools/lab-devOps/scripts/matlab/rmat.sh [--parallel] <your-script-name>
```

Notes:
- `<your-script-name>` is the name of your ".m" file, but without the file extension
- you can optionally attached the `--parallel` flag to specify that this job requires parallel processing

This will generate an Slurm script called ????.sub. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

## MATLAB GUI
TBD.