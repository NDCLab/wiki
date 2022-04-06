---
layout: default
title: R
parent: HPC
nav_order: 2
---

### Contents
1. [Running R](#Running-R)
    1. [Packages](#Loading-Packages)
    2. [Running](#Running-Scripts)
2. [RStudio](#RStudio)

## Running R

To run scripts in the R programming language using the login node, follow the steps listed below:

### Packages

Located in `/home/data/NDClab/tools/containers/R-4.1.2/` is a default container that contains all environment variables and packages requried to run any R script. Below we will explore how we can use this container to run your R script.

### Running

To run your R script, execute the following command in your terminal.

```
sh /home/data/NDClab/tools/lab-devOps/rrun.sh <file_name>.R
```

This will generate an sbatch script, submit it, and return an output to your folder location.

## RStudio