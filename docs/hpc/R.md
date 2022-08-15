---
layout: default
title: R
parent: HPC
nav_order: 5
---

### Contents
1. Packages(#packages)
2. Running an R Script(#running-an-r-script)
3. [RStudio](#rstudio)


## Packages
Located in `/home/data/NDClab/tools/containers/R-4.1.2/` is a default container that contains all environment variables and packages required to run any R script.

You can access the recipe file named `R.recipe`. 

On line 85 is a line instructing R to install a number of packages. If your script requires a package that is not listed here, you will need to create a new container.



## Running an R Script

To run scripts in the R programming language using the login node, execute the following command in your shell:

```
sh /home/data/NDClab/tools/lab-devOps/scripts/R/rrun.sh <file_name>.R
```

This will generate an sbatch script, submit it, and return an output to your folder location.

After you initially run `rrun.sh`, you should subsequently run the sbatch file generated in your folder via:

```
sbatch <file_name>.sub
```

## RStudio