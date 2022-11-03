---
layout: default
title: Matlab
parent: HPC
nav_order: 4
---

### Contents
1. [Running Matlab](#Running-Matlab)
    1. [Running](#Running-Scripts)
2. [Matlab GUI](#Matlab-GUI)

## Running Matlab

To run scripts in the Matlab programming language using the login node, follow the steps listed below:

### Running

To run your matlab script, execute the following command in your terminal.

```
sh /home/data/NDClab/tools/lab-devOps/scripts/matlab/rmat.sh [--parallel] <file_name>
```

Optionally, you can attach the *--parallel* flag to specify that this job requires parallel processing.

This will generate an sbatch script, submit it, and return an output to your folder location.

After you initially run `rmat.sh`, you should subsequently run the sbatch file generated in your folder via:

```
sbatch <file_name>.sub
```

## Matlab-GUI