---
layout: default
title: R
parent: HPC
nav_order: 5
---

### Contents
1. [Running R](#Running-R)
    1. [Packages](#Loading-Packages)
    2. [Adding Packages](#Modifying-Packages)
    3. [Running](#Running-Scripts)
    4. [Data Parallelization](#Data-Parallels)
2. [RStudio](#rstudio)

## Packages
Located in `/home/data/NDClab/tools/` is the lab's current default singularity image for R; it contains all environment variables and packages required to run any R script.

You can access the recipe file named `R.recipe`. [Log in](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node), then download this file and open it in a text editor on your local machine.

Near the bottom is a line instructing R to install a number of packages:

```yml
R --no-echo -e 'install.packages(c("Rcpp", "DEoptim", "ggplot2", "data.table", "dplyr", "tidyr", "knitr", "readxl"))'
```

If your script requires a package that is not listed here, a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html) will need to be created.



## Running an R Script
To run a script in the R programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
sh /home/data/NDClab/tools/lab-devOps/scripts/R/rrun.sh <your-script-name>.R
```

This will generate an Slurm script named after your script: `your-script-name.sub`. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).

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

## RStudio
TBD
