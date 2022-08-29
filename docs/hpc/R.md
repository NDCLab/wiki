---
layout: default
title: R
parent: HPC
nav_order: 5
---

### Contents
1. [Packages](#packages)
2. [Running an R Script](#running-an-r-script)
3. [RStudio](#rstudio)


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

## RStudio
TBD