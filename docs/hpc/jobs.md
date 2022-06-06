---
layout: default
title: Job Submission
parent: HPC
nav_order: 5
---

### Contents
1. [Overview](#overview)
2. [Creating a Slurm File](#creating-a-slurm-file)
3. [Running a Slurm File](#running-a-slurm-file)


## Overview
For anything that goes beyond running basic lines of code, a job must be submitted to the compute nodes so that the compute nodes can properly handle tasks. Note, this is a **requirement** on the HPC, as login nodes are not the intended resource for computation.

## Creating a Slurm File
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

## Running a Slurm File
To run an existing slurm file, you will log into the HPC and utilize the [shell](https://ndclab.github.io/wiki/docs/technical-docs/shell.html) interface to execute the script.
1. First, make sure that you are connected to the FIU VPN using your personal credentials. Follow the instructions [here](https://fiu.service-now.com/sp?id=kb_article&sys_id=6c3c789ddb899780b16af969af96193d).
2. Using Google Chrome as your browser, visit [hpcgui.fiu.edu](hpcgui.fiu.edu) and log in with your personal credentials.
3. Under Clusters, select "Panther Shell Access."
![shell-access](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/shell-access.png)
4. When prompted, input your password. (It will no look like you are typing anything, but persever and hit Enter!)
5. Navigate to the folder containing the slurm file (file extension `.sub`) that you want to execute using `cd` commands.
6. Run the script by typing the following into the shell: `sbatch <filename.sub>`. For instance, to execute a hallMonitor.sub file, you would type `sbatch hallMonitor.sub`.
7. The shell will output a message to indicate that the batch was submitted and its associated job number:
![sbatch-submit](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/sbatch-submit.png)
8. Use `ls` to see if the process is complete. When it is complete, you will see an output file in the same folder whose name is "slurm-NUMBER.out":
![sbatch-output](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/sbatch-output.png)
9. Use `cat slurm-NUMBERS.out` to print all messages to the console.
