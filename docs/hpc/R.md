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
    4. [Data Parallelization](#Data-Parallels)

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
### Data Parallels

Data parrallelization, at the current iteration of the HPC, is unsupported in R. Namely, the [mpi](https://hpc-wiki.info/hpc/MPI) library is not installed to this HPC. So, if we would like to run data in parallel we would have to engineer our own solution.

As each dataset has its own parameters and contexts, a general script is not available for use.

However, a template script is available in `/hpc/data/NDClab/tools/lab-devOps/R/data-par/parallel-nodes.sh`

This script works by taking in 2 parameters: `nodes` and `data`. `nodes` describes how many nodes we would like to utilize for parallel-development & which `data` file we would like to parallelize. For example, this script:

```s
sh /hpc/data/NDClab/tools/lab-devOps/R/data-par/parallel_nodes.sh 8 filename.csv
```

would split `filename.csv` into 8 seperate files that will be run in parallel.

Specifically, it executes the `do_node.sh` script on 8 equal sections of our data. To control which script is being run on each portion of data, we will need to modify the script located at `do_node.sh`:

```
Rscript <SCRIPTHERE> $data
```
