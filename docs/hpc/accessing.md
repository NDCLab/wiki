---
layout: default
title: Accessing the HPC
parent: HPC
nav_order: 2
---

![cluster visualization](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/cluster.png)
*Visualization by Yale Center for Research Computing*

### Contents
1. [Connecting](#connecting)
2. [Access Methods](#access-methods)
    1. [Login Node](#login-node)
    2. [Visual Node](#visual-node)
2. [Structure](#structure)
3. [Relationship with GitHub](#relationship-with-github)

## Connecting
To use the HPC, a lab member must either use:
- on-campus WiFi
- the [FIU VPN](https://network.fiu.edu/vpn/) to access the [FIU intranet](https://en.wikipedia.org/wiki/Intranet). Instructions are available [here](https://fiu.service-now.com/sp?id=kb_article&sys_id=6c3c789ddb899780b16af969af96193d).

Once connected to either on-campus WiFi or the VPN, use Google Chrome to access the site [hpcgui.fiu.edu](hpcgui.fiu.edu).


## Access Methods
### Login Node
The login node, also known as the head node, is the primary HPC entry point for submitting jobs and transferring small amounts of data.

From the HPC GUI login page, select "Clusters," then "Panther Shell Access;"
![shell-access](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/shell-access.png)

When prompted, input your password. (It will no look like you are typing anything, but persevere and hit Enter!)

A prompt will indicate a successful login:
```
#######################################################################
Welcome to the FIU Instructional & Research Computing Center (IRCC)
#######################################################################
```

From here, you can use the command line as you would use any [shell](https://linuxcommand.org/lc3_lts0010.php). You can also submit batch jobs to the compute-node with the ["sbatch" command](https://ndclab.github.io/wiki/docs/hpc/jobs.html).

If you are feeling fancy, you can access this directly without logging in via the browser.  Simply open your local shell and type:
```
ssh YOURLOGIN@hpclogin01
```

You will be prompted to input your password, and then you can navigate the HPC as you would on the browser. To return to using your shell to access files on your local computer, simply execute an `exit` command.  (Note: this method is called "secure shell (SSH), which comes pre-installed on Windows10 and MacOS. Older Windows versions are available for install [here](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse).)

### Visual Node
The visualization node is used for directly editing files on the cluster and for GUI manipulation. There are two options:
- the file navigator
- an interactive desktop

The file navigator is similar to a Windows Explorer or Mac Finder type interface. It is useful for viewing folder structure and contents from a high level.

If more interactive access is required, for instance downloading Pavlovia data and uploading to the HPC, this can be accomplished on the interactive desktop. The desktop is resource intensive, so it is best reserved for the kinds of operations that cannot be accomplished via the shell or file navigator.


## Structure

The NDCLab follows the structure listed below.
![NDCLab_privileges drawio](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/NDCLab_privileges.drawio.png)

The left and right diagrams represent the read, write, and execute permissions for a general lab member and a lab member attached to a given project, respectively. Each color corresponds to the following group:

![colorcode](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/hpc/Privileges_legend_transparent.drawio.png)

All lab members are part of the NDCLab and have read access to the labs' projects, including datasets, analyses, and tools, but only a select few members are part of a specific project. This results in specific privileges given to select members to ensure data compliance. For example, a lab member has read and execute privileges for any public data on the cluster, but only "Project-A" lab members will be able to read and execute the private section of `data/project-A/` as well as write files and code to the project repository. Write permissions to a project's private data and data derivatives are handled on a case-by-case basis depending on the lab member's role in the project.

The main directories -- `datasets`, `tools`, and `analyses` -- are described below.

### datasets
Data collection projects have a directory in this folder to house de-identified and encrypted data. Project leads, approved project members, and lab staff have read and write access to the entire directory, while lab members who are not involved in the project are able to view publicly-available data.

In addition, publicly-available datasets may be replicated to their own directories for additional analyses to be performed by lab members.

### tools
This folder contains various scripts and software utilized within the lab for organization, data monitoring, and compliance checking. 

### analyses
Analysis projects have a directory in this folder to house analysis scripts and their derivatives, such as statistics, plots, and completed products.


## Relationship with GitHub
Wherever possible, the NDCLab endeavors to operate as a fully open lab, providing public access to our ongoing projects. For this reason, all dataset and analysis directories on the HPC are, in fact, mirrors of a GitHub repository.

Information that is pushed to the `main` branch of the GitHub repository is mirrored to the associated HPC folder at 1 am EST nightly. This connection is **one-way**: that is, for the purposes of data security, data on the HPC is **not** mirrored back to GitHub. In addition, the `sourcedata` and `derivatives` folders of dataset directories/repositories are explicitly ignored by Git.

If an immediate sync of an HPC directory to the GitHub remote is required, this can be achieved with a `git pull` from the HPC shell.
