---
layout: default
title: R
parent: HPC
nav_order: 5
---

### Contents
1. [Packages](#packages)
2. [Running an R Script](#running-an-r-script)
3. [Parallelization](#parallelization)


## Packages
Located in `/home/data/NDClab/tools/containers` is the lab's current default singularity image for R; it contains all environment variables and packages required to run an R script.

You can access the recipe file named `R.recipe`. [Log in](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node), then download this file and open it in a text editor on your local machine.

Near the bottom is a line instructing R to install a number of packages:

```yml
R --no-echo -e 'install.packages(c("Rcpp", "DEoptim", "ggplot2", "data.table", "dplyr", "tidyr", "knitr", "readxl"))'
```

If your script requires a package that is not listed here, a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html) will need to be created.


## Running an R Script
To run a script in the R programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/R/rrun.sh <your-script-name>.R [# nodes] [hours of walltime requested]
```

By default the script will call for 1 hour of walltime (time required to execute the script) and 1 node. If walltime needed or nodes desired exceeds 1 hourand 1 node the arguments [# nodes] [hours of walltime requested] should be included (i.e. <your-script-name>.R 1 24 calls for 1 node and 24hrs walltime).

This will generate and run a Slurm script named after your script: `your-script-name.sub`. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).


## Parallelization
Data parallelization, at the current iteration of the HPC, is unsupported in R. Namely, the [mpi](https://hpc-wiki.info/hpc/MPI) library is not installed to this HPC. So, if we would like to run data in parallel, we would need to engineer our own solution.

As each dataset has its own parameters and contexts, a general script is not available for use.

However, a template script is available in `/hpc/data/NDClab/tools/lab-devOps/R/data-par/parallel-nodes.sh`

This script works by taking in 2 parameters: `nodes` and `data`. These parameters describe how many `nodes` we would like to utilize for parallel development and which `data` file we would like to parallelize. For example, this script:

```s
sh /hpc/data/NDClab/tools/lab-devOps/R/data-par/parallel_nodes.sh 8 filename.csv
```

would split `filename.csv` into 8 seperate files that would be run in parallel.

Specifically, it executes the `do_node.sh` script on 8 equal sections of our data. To control which script is being run on each portion of data, we will need to modify the line bellow, located in `do_node.sh`:

```
Rscript <SCRIPTHERE> $data
```
