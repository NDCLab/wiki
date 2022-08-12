---
layout: default
title: R
parent: HPC
nav_order: 2
---

### Contents
1. [Running R](#Running-R)
    1. [Packages](#Loading-Packages)
    2. [Adding Packages](#Modifying-Packages)
    3. [Running](#Running-Scripts)
    4. [CPU Parallelization](#CPU-Parallels)
    5. [Data Parallelization](#Data-Parallels)
    6. [Combining The Two](#Combining)
2. [RStudio](#RStudio)

## Running R

To run scripts in the R programming language using the login node, follow the steps listed below:

### Packages

Located in `/home/data/NDClab/tools/containers/R-4.1.2/` is a default container that contains all environment variables and packages requried to run any R script. Below we will explore how we can use this container to run your R script.

### Packages

To add a package to this R container, you can access the recipe file named `R.recipe`. 

On line 85 is a line instructing R to install a number of packages. If you do not see a package required for your code simply add your package name to this list and rebuild the container image in a Linux environment with root access.

### Running

To run your R script, execute the following command in your terminal.

```
sh /home/data/NDClab/tools/lab-devOps/scripts/R/rrun.sh <file_name>.R
```

This will generate an sbatch script, submit it, and return an output to your folder location.

After you initially run `rrun.sh`, you should subsequently run the sbatch file generated in your folder via:

```
sbatch <file_name>.sub

```
### CPU Parallels


### Data Parallels


### Combining

## RStudio