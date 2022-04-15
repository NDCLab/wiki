---
layout: default
title: Job Submission
parent: HPC
nav_order: 5
---

For anything that goes beyond running basic lines of code, a job must be submitted to the compute nodes so that the compute nodes can properly handle tasks. Note, this is a **requirement** on the HPC, as login nodes are not the intended resource for computation.

To create a job, a [slurm](https://slurm.schedmd.com/documentation.html) file must be created. The file below represents a sample Slurm script where a conda base environment is being activated: 

```yml
#!/bin/bash

#SBATCH --job-name=myjob         # create a short name for your job
#SBATCH --nodes=1                # node count
#SBATCH --ntasks=1               # total number of tasks across all nodes
#SBATCH --time=00:01:00          # total run time limit (HH:MM:SS)
#SBATCH --mail-type=end          # send email when job ends

module load miniconda3-4.5.11-gcc-8.2.0-oqs2mbg

conda exec -b base python sample.py
```