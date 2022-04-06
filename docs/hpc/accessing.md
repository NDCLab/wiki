---
layout: default
title: Accessing the HPC
parent: HPC
nav_order: 1
---

![cluster visualization](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/cluster.png)
*Visualization by Yale Center for Research Computing*


### Contents
1. [Connecting](#Connecting)
    1. [Login Node](#Login-Node)
    2. [Visual Node](#Visual-Node)
2. [Structure](#Structure)

## Connecting
To use the HPC, a lab member must either use on-campus WiFi or utilize a VPN to access the [FIU intranet](https://en.wikipedia.org/wiki/Intranet). 

Once a secure connection is established, both the login node and visual nodes can be accessed for job submission and file manipulation.

### VPN (Off-Campus Only!)
If a lab member is using on-campus WiFi, this step can be skipped. 

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

The NDCLab follows the structure listed below.

![NDCLab Privilges](https://user-images.githubusercontent.com/26397102/122823863-dfbfdb80-d2ad-11eb-94b8-daf9a585f890.png)

The left and right diagrams represent the varying read & execute privileges and the write privileges respectively. Each color corresponds to the following group:

![colorcode](https://user-images.githubusercontent.com/26397102/122824230-607ed780-d2ae-11eb-81bc-93011d4569c4.png)

All lab members are part of the NDCLab, but only a select few members are part of a specific project. This results in specific privileges given to select members to ensure data compliance. For example, a lab member has read and execute privileges for any public data on the cluster, but only "Project-A" lab members will be able to read and execute the private section of `data/project-A/`. 

The main directories -- `datasets`, `tools`, and `analyses` -- are described below.

### datasets
Each project has a directory in this folder to house de-identified and encrypted data.

Project leads, approved project members, and lab staff will have sole read and write access to the entire directory, while external lab members will be able to only view publicly-available data. 

### tools
This folder contains various scripts and software utilized within the lab for organization, preprocessing, and compliance checking. 

### analyses
Finally, each ongoing project has a folder in the `analyses` directory, which contains cleaned datasets, plots, and various statistics.