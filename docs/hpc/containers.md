---
layout: default
title: Containers
parent: HPC
nav_order: 6
---

### Contents
1. [Installation](#Setting-Up)
2. [Building Your Own Container](#Building-Your-Own-Container)
3. [Transferring](#Transferring)

## Setting Up

To build your own singularity container for use in the shared HPC, you will need to install the following software and OS installations:

* [Oracle VM Box](https://www.virtualbox.org/wiki/Downloads)
* [Red Hat OS](https://developers.redhat.com/products/rhel/download)

To load this OS onto your VM box, follow along with the [guided tutorial](https://www.youtube.com/watch?v=hE2eOLx0gNU).

## Building Your Own Container

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

Once you've created this file, you will execute:

```
sudo singularity build container.recipe container.simg
```

This will create a new singularity container with all your required Python packages.

## Transferring

Lastly, you will transfer this container by uploading it via [hpcgui.fiu.edu](hpcgui.fiu.edu). 


