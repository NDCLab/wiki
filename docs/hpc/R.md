---
layout: default
title: R
parent: HPC
nav_order: 5
---

### Contents
1. [Running an R Script](#running-an-r-script)
2. [Packages](#packages)
3. [Parallelization](#parallelization)

## Running an R Script
To run a script in the R programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. You can run your R script within an R module on the HPC (e.g. `module load r-4.4.1-gcc-13.2.0`, use `module avail r` to see available modules) or, if you require packages not included in this module you can use one of the existing R Singularity containers in `/home/data/NDClab/tools/containers/R` that have your required packages, or create a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html).

### Using R Module
From that location, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/R/rrun.sh <your-script-name>.R [# nodes] [hours of walltime requested]
```

By default the script will call for 1 hour of walltime (time required to execute the script) and 1 node. If walltime needed or nodes desired exceeds these defaults, then the arguments [# nodes] [hours of walltime requested] should be included (i.e. `<your-script-name>.R 1 24` calls for 1 node and 24hrs walltime).

This will generate and run a Slurm script named after your script: `your-script-name.sub`. If you want to re-run the script, you can re-run the .sub file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file). Once the script is created you can go in and manually edit parameters you want to change.

### Using Singularity Image
Using a Singularity image, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/R/rrun_container.sh <your-script-name>.R [# nodes] [hours of walltime requested]
```

Like with `rrun.sh` this will generate and run a Slurm script `your-script-name.sub`, with [# nodes] and [hours walltime] as specified in the command above, that runs your R code within a Singularity image.

## Packages
R scripts often require numerous packages, that have to be the correct versions, and so you need to make sure that the Singularity image or R module you're running the script within has the packages required.

Located in `/home/data/NDClab/tools/containers` is the lab's current default singularity image for R; it contains all environment variables and packages required to run an R script.

You can access the recipe file named `R.recipe`. [Log in](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node), then download this file and open it in a text editor on your local machine.

Near the bottom is a line instructing R to install a number of packages:

```yml
R --no-echo -e 'install.packages(c("Rcpp", "DEoptim", "ggplot2", "data.table", "dplyr", "tidyr", "knitr", "readxl"))'
```

Alternatively, if you're using the R module on the HPC, you can open R and run `installed.packages()` to view which packages are installed on the module you're using.

If your script requires a package that is not listed here, a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html) will need to be created.


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
