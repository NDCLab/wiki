---
layout: default
title: HPC
parent: Technical Documentation
nav_order: 3
---

![dt2-racks-from-front](https://user-images.githubusercontent.com/26397102/118044340-27148d00-b33c-11eb-8b2c-17a454f18c51.jpg)  
*Not the FIU cluster*

## Outline 

* [Introduction](#introduction)
* [Connecting to the HPC](#connecting)
    * [Establishing VPN Connection](#vpn)
    * [Login Node](#login-node)
    * [Visual Node](#visual-node)
* [HPC File Structure](#Structure)
* [Git](#git)
* [Singularity](#singularity)
* [Slurm](#slurm)
* [Jupyter](#jupyter)  

## Introduction
The [FIU High-performance computing (HPC) cluster](http://ircc.fiu.edu/) is a group of interconnected computers designed to perform computationally "expensive" tasks. This includes processing large quantities of data and executing programs in parallel. 

While a personal computer with 6 cores could execute 6 programs in parallel, one of the 3000 compute nodes in the HPC cluster could execute 44 programs in parallel.

The following document details how to access and properly utilize this resource, **assuming an HPC account is granted**. Lab members must be [onboarded to the HPC](https://ndclab.github.io/wiki/docs/Onboarding/accessing-hpc.html) by the lab manager.



## Connecting
To use the HPC, a lab member must either use on-campus WiFi or utilize a VPN to access the [FIU intranet](https://en.wikipedia.org/wiki/Intranet). 

Once a secure connection is established, both the login node and visual nodes can be accessed for job submission and file manipulation respectively.

### VPN
If a lab member is using on-campus WiFi, this step can be safely skipped. 

However, if a lab member is accessing the HPC off-campus, they must connect to the [FIU VPN](https://network.fiu.edu/vpn/) to access the FIU intranet. 

### Login-Node 
The login node, also known as the head node, is the primary HPC entry point for submitting jobs and transferring small amounts of data.

Note: a user must login to the login-node **before** logging into the hpcgui to initialize their home directory. 

The preferred (and easiest) method for accessing the HPC login node is through secure shell (SSH). This comes installed on Windows 10 and MacOS. Previous windows versions can install [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse).

Verify your ssh installation by typing in the command prompt/terminal. 
```
ssh -v localhost 
```

1. Once verified, ssh into the login node, Where `userName` is the lab member's FIU username:
```
ssh userName@hpclogin01
```

2. Enter the password when prompted:
```
userName@hpclogin01 password:
```


3. A prompt will indicate a successful login:
```
#######################################################################
Welcome to the FIU Instructional & Research Computing Center (IRCC)
#######################################################################
```

### Visual-Node
The visualization node is used for directly editing files on the cluster and for GUI manipulation. To access the visual node, simply click [hpcgui.fiu.edu](hpcgui.fiu.edu).

<img width="957" alt="fiuHPCgui" src="https://user-images.githubusercontent.com/26397102/119862076-c067a580-bedd-11eb-9481-b1d6ca42b554.png">

The red boxes detail the following:

* Files: represent a graphical representation of the file structure on the cluster
* Clusters: provide [shell](https://ndclab.github.io/wiki/docs/shell) access to the cluster
* Interactive Apps: GUI applications available for HPC account-holders 

## Structure

Within the cluster, the NDCLab will have the following file structure:

![NDCLab Privilges](https://user-images.githubusercontent.com/26397102/122823863-dfbfdb80-d2ad-11eb-94b8-daf9a585f890.png)

The left and right diagrams represent the varying read & execute privileges and the write privileges respectively. Each color corresponds to the following group:

![colorcode](https://user-images.githubusercontent.com/26397102/122824230-607ed780-d2ae-11eb-81bc-93011d4569c4.png)

All lab members are part of the NDCLab, but only a select few members are part of a specific project. This results in specific privileges given to select members to ensure data compliance. For example, a lab member has read and execute privileges for any public data on the cluster, but only "Project-A" lab members will be able to read and execute the private section of `data/project-A/`. 

The main directories -- `data`, `scripts`, and `analyses` -- are described below.

### data
Each project has a directory in this folder to house de-identified and encrypted data.

Project leads, approved project members, and lab staff will have sole read and write access to the entire directory, while external lab members will be able to only view publicly-available data. 

### scripts
Similarily, each project has a directory in `scripts` that contains pertinent code cloned in from GitHub. This code is updated daily via [cron](https://en.wikipedia.org/wiki/Cron), but can be manually updated `git pull` if the need arises. 

The additional `devOps` folder contains scripts used for lab-wide cluster organization. 
### analyses
Finally, each ongoing project has a folder in the `analyses` directory, which contains cleaned datasets, plots, and various statistics.

## Git
By default, [Git](https://ndclab.github.io/wiki/docs/git-and-github) comes installed on the HPC cluster. However, without properly configuring an email address and user name, and linking a GitHub account, users have read-only privileges when it comes to cloning or forking from GitHub. 

To link a GitHub account to the HPC, follow the steps outlined the FIU Neuro Onboarding [link](https://github.com/fiuneuro/Onboarding#setting-up-git-on-the-hpc). 

## Singularity
Singularity is the preferred container to use on the FIU HPC cluster, as an improperly secured Dockerfile can grant root access to a system it is running on.

However, Dockerfiles can be used with Singularity on the HPC, and making the jump between the two is trivial.

## Using Dockerfile with Singularity

If the singularity file has not already been created on the cluster, but a dockerfile image exists, then follow the steps outlined below: 

1. After building the intended image to use with Singularity, run the following command to view the Image ID. 
```
docker images
```

2. Next, save the image as a .tar file by running where <IMAGEID> is the id of the docker file (this may take a while!).
```
docker save <IMAGEID> -o <myImage>.tar 
```

3. Unless running on a linux machine or vm, singularity will not be available to your local. Instead transfer the .tar file to the HPC cluster.
```
scp <myImage>.tar <YourID>@hpclogin01:images
```

4. SSH into the FIU cluster and move the file to the appropriate path (wherever the project itself is on the cluster).
```
ssh <YourID>@hpclogin01
cd images
mv <myImage>.tar <path/to/project>
```

5. And lastly, build the singularity image.
```
singularity build <myImage>.sif docker-archive://<myImage>.tar
```

## Slurm
For anything that goes beyond running basic lines of code, a job must be submitted so that the compute nodes can properly handle tasks. Note, this is a **requirement** on the HPC, as login nodes are not the intended resource for computation.

<span style="color:red">Repeated improper utilization of login node resources can lead to a ban from the cluster.</span>

![Napoleon_inexile](https://user-images.githubusercontent.com/26397102/124790916-94e2cc80-df19-11eb-89e6-7281c5980101.jpg)  
*"if only I used slurm more often"*

To create a job, a [slurm](https://slurm.schedmd.com/documentation.html) file must be created. The file below represents a sample Slurm script where a conda base environment is being activated: 

```yml
#!/bin/bash
#SBATCH --qos medium
#SBATCH --account iacc_gbuzzell
#SBATCH --partition 6g-per-core

#SBATCH --job-name=myjob         # create a short name for your job
#SBATCH --nodes=1                # node count
#SBATCH --ntasks=1               # total number of tasks across all nodes
#SBATCH --time=00:01:00          # total run time limit (HH:MM:SS)
#SBATCH --mail-type=end          # send email when job ends
#SBATCH --mail-user=<YourID>@fiu.edu

. $MODULESHOME/../global/profile.modules
module load miniconda3-4.5.11-gcc-8.2.0-oqs2mbg
conda activate

python sample.py
```

The first 3 lines of the script specify the "private" queue used for the lab.  Always specify 'medium' and select one of the medium machines.

## Jupyter

To use a Jupyter Notebook on the HPC:
   
1. Launch the Panther desktop from the [HPC desktop](https://wwww.hpcgui.fiu.edu):

<img src="https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/launching-panther-desktop.png" width="800" height="400">


2. Once the desktop has launched, open the terminal. Load conda, then jupyter.

<img src="https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/terminal-actions-conda-jupyter.png" width="800" height="300">

Note: we use a [conda environment](http://ircc.fiu.edu/custom-environments-and-package-installation-r-and-python/) for our scripts for version control. (We do not use pip.)
