---
layout: default
title: Matlab
parent: HPC
nav_order: 6
---

### Contents
1. Packages(#packages)
2. Running a MATLAB Script(#running-a-matlab-script)
3. [MATLAB GUI](#matlab-gui)


## Packages


## Running a MATLAB Script
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

## MATLAB GUI