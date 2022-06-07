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
To create a job, a [slurm](https://slurm.schedmd.com/documentation.html) file must be created:
1. First, make sure that you are connected to the FIU VPN using your personal credentials. Follow the instructions [here](https://fiu.service-now.com/sp?id=kb_article&sys_id=6c3c789ddb899780b16af969af96193d).
2. Using Google Chrome as your browser, visit [hpcgui.fiu.edu](hpcgui.fiu.edu) and log in with your personal credentials.
3. Under Clusters, select "Panther Shell Access."
![shell-access](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/shell-access.png)
4. When prompted, input your password. (It will no look like you are typing anything, but persever and hit Enter!)
5. Navigate, using `cd` commands, to the folder where you want to place the slurm file.
6. Create and open a new file with the command `nano USEFULNAME.sub` where USEFULNAME is replaced by an actually useful name that describes what this .sub file will do.
7. Type or paste into the empty file the necessary script information. See below for an example that can be customized.
8. Save your new file by holding down the ctrl key and pressing the letter 'o'. (Note: this is ctrl on both PC and Mac, not cmd.) You will be prompted to save the file, which you do by hitting enter/return.
9. To exit the nano view, hold down the ctrl key again and press the letter 'x'.
10. Use `ls` to inspect the contents of the folder. You should see your new .sub file.

The file below represents a sample Slurm script where a conda base environment is being activated: 

```yml
#!/bin/bash

#SBATCH --job-name=myjob         # job name
#SBATCH --nodes=1                	# node count
#SBATCH --ntasks=1               	# total number of tasks across all nodes
#SBATCH --time=00:24:00          	# total run time limit (HH:MM:SS)
#SBATCH --mail-type=end          	# send email when job ends

module load miniconda3-4.5.11-gcc-8.2.0-oqs2mbg

conda exec -b base python sample.py
```

Here is a guide to what these details in the .sub file mean and how they should be customized:
| variable/text  | description  | how to customize  |
| :--  | :--  | :--  |
| #!/bin/bash  | tells the HPC to read what follows in the Bash language  | Do not modify.  |
| job-name  | name for the job  | how to customize  |
| nodes  | tells the HPC how many nodes should be utilized (nodes are individual computers in the cluster)  | how to customize  |
| nodes  | tells the HPC how many tasks (that is, CPUs) should be utilized across nodes selected | how to customize  |
| time  | limits the amoount of time the HPC should devote to running the script  | how to customize  |
| mail-type  | tells the HPC to send you an e-mail when the job is done  | If the job is very small and will run quickly, you can delete this line to avoid an unnecessary e-mail in your inbox. Otherwise, leave it unchanged.  |
| module load miniconda3-4.5.11-gcc-8.2.0-oqs2mbg  | Loads a specific version of conda, R, etc.  | how to customize  |
| conda exec -b base python sample.py  | the actual command to run the script specified  | how to customize  |


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
