---
layout: default
title: Containers
parent: HPC
nav_order: 4
---

### Contents
1. [Overview](#overview)
2. [Default Lab Container](#default-lab-container)
3. [Building a New Container](#building-a-new-container)


## Overview
Containers are used to ensure reproducibility of results. In essence, they are a miniature "world" that contains specific versions of the software and packages you are using. If anyone runs your code within the same container as you used, they should get the same results.


## Default Lab Container
Before calling a container, check that the lab default contains all packages that you need. If your script uses a package that isn't included in the container, you may want to simply swap out for a similar package that is already in the container. If you cannot swap, you will need a new container.

## Building a New Container
To build a brand new container, follow the instructions below.

### Set Up

To build your own singularity container for use in the shared HPC, you will need to install the following software and OS installations:

* [Oracle VM Box](https://www.virtualbox.org/wiki/Downloads)
* [Red Hat OS](https://developers.redhat.com/products/rhel/download)

To load this OS onto your VM box, follow along with this [guided tutorial](https://www.youtube.com/watch?v=hE2eOLx0gNU).

### Build

Once you have your RedHat OS successfully installed, you will utilize the following "recipe" file template to build an R or Python container.

Copy and paste the text below into a file called `container.recipe`.

```sass
Bootstrap: docker
From: ubuntu:20.04

%help

	.__   __.  _______   ______  __          ___      .______   
	|  \ |  | |       \ /      ||  |        /   \     |   _  \  
	|   \|  | |  .--.  |  ,----'|  |       /  ^  \    |  |_)  | 
	|  . `  | |  |  |  |  |     |  |      /  /_\  \   |   _  <  
	|  |\   | |  '--'  |  `----.|  `----./  _____  \  |  |_)  | 
	|__| \__| |_______/ \______||_______/__/     \__\ |______/  
                                                            
	Start this container to reliably run the base-eeg pipeline with all
	necessary packages, environments, and libraries. 

	Usage:
	
	To start a shell instance with the container image, execute
		
		singularity shell container/run-container.simg

	To execute a command within the container, execute:
		
		singularity exec container/run-container.simg [command]

	Lastly, to create an instance of the container that runs in the 
	background, execute:

		singularity instance start container/run-container.simg [name]

	Commands can be passed to the instance using the following format

		singularity exec instance://[name] [command]

	To submit an issue visit https://github.com/NDCLab/baseEEG. We 
	encourage open-source collaboration!

%files
	
	requirements.txt

%post

	export DEBIAN_FRONTEND=noninteractive
	
	# update package list and install tools
	apt-get update --allow-releaseinfo-change && apt-get install -y  \
 	 build-essential \
 	 bash-completion=1:2.10-1ubuntu1 \
 	 golang=2:1.13~1ubuntu2 \
 	 locales=2.31-0ubuntu9 \
 	 python3-pip=20.0.2-5ubuntu1.6 \
 	 sudo=1.8.31-1ubuntu1.2 \
 	 nano=4.8-1ubuntu1 \
	 && rm -rf /var/lib/apt/lists/* && apt-get clean

	# set time
	locale-gen en_US.UTF-8
	
	# install python packages
	pip3 install -r requirements.txt

	# create user and set as sudo
	adduser --disabled-password --gecos '' ndc
	adduser ndc sudo
	echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
	su ndc

```

Your `requirements.txt` file will contain all the [necessary packages](https://learnpython.com/blog/python-requirements-file/) for your Python container.

(To add a package to the existing Python container, you can access the recipe file named `python.recipe`. On line 61 is a line instructing the container to install a number of Python modules from the `requirements.txt` file. If you do not see a package required for your code simply add your package name to this file and rebuild the container image in a Linux environment with root access.

To add a package to the existing R container, you can access the recipe file named `R.recipe`. On line 85 is a line instructing R to install a number of packages. If you do not see a package required for your code simply add your package name to this list and rebuild the container image in a Linux environment with root access.)

Once you've created this file, load singularity and execute the following command:

```
singularity build --remote container.simg container.recipe 
```

You may need to create a singularity account to execute this command. Sign up at [Sylabs](cloud.sylabs.io). If you see that you need a token or your token is expired, you can generate a new one [here](clous.sylabs.io/auth/tokens). Then you should be able to login:
```
singularity remote login
```
...with your token and execute the build command above to create a new singularity container "container.simg" with all your required Python packages.

### Transfer

Lastly, upload this container to the lab's "containers" (tools/containers) directory via [hpcgui.fiu.edu](hpcgui.fiu.edu). 
