---
layout: default
title: R
parent: HPC
nav_order: 3
---

### Contents
1. [Running Python](#Running-Python)
    1. [Packages](#Loading-Packages)
    2. [Adding Packages](#Modifying-Packages)
    3. [Running](#Running-Scripts)
    4. [CPU Parallelization](#CPU-Parallels)

## Running R

To run scripts in the Python programming language using the login node, follow the steps listed below:

### Packages

Located in `/home/data/NDClab/tools/containers/python-3.8/` is a default container that contains all environment variables and packages requried to run any Python script. Below we will explore how we can use this container to run your Python script.

### Packages

To add a package to this Python container, you can access the recipe file named `python.recipe`. 

On line 61 is a line instructing the container to install a number of Python modules from the `requirements.txt` file. If you do not see a package required for your code simply add your package name to this file and rebuild the container image in a Linux environment with root access.

### Running

To run your python script, execute the following command in your terminal. Be sure that you are in the directory of `file_name`.py when running this script.

```
sh /home/data/NDClab/tools/lab-devOps/scripts/python/prun.sh <file_name>.py
```

This will generate an sbatch script, submit it, and return an output to your folder location.

After you initially run `prun.sh`, you should subsequently run the sbatch file generated in your folder via:

```
sbatch <file_name>.sub

```
### CPU Parallels

To take advantage of the HPC's multiple nodes, utilize the multiprocessing module. Consult the documentation [here](https://docs.python.org/3/library/multiprocessing.html) to get started.

To quickly set up multiprocessesing functionality, you can utilize

```python
from multiprocessing import Pool
```

which will create a "worker" for each available CPU that you utilize.

