---
layout: default
title: Python
parent: HPC
nav_order: 7
---

### Contents
1. [Running a Python Script](#running-a-python-script)
2. [Packages](#packages)
3. [Parallelization](#parallelization)

## Running a Python Script
To run a python script using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. You then have the choice to run your Python script using a miniconda Python module available on the HPC (`module avail miniconda`), or, if you require other packages not included in this module, you can use one of the existing Python Singularity containers in `/home/data/NDClab/tools/containers` that have your required packages, or create a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html).


### Using Miniconda Module

From that location, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/python/prun.sh <your-script-name>.py [# nodes] [hours of walltime requested]
```

By default the script will call for 1 hour of walltime (time required to execute the script) and 1 node. If walltime needed or nodes desired exceeds these defaults, then the arguments [# nodes] [hours of walltime requested] should be included (i.e. `<your-script-name>.py 1 24` calls for 1 node and 24hrs walltime).

This will generate and run a Slurm script named after your script: `your-script-name.sub`. If you want to re-run the script, you can re-run the .sub file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file). Once the script is created you can go in and manually edit parameters you want to change.

### Using Singularity Image

Using a Singularity image, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/python/prun_container.sh <your-script-name>.py [# nodes] [hours of walltime requested]
```

Like with `prun.sh` this will generate and run a Slurm script `your-script-name.sub`, with [# nodes] and [hours walltime] as specified in the command above, that runs your Python code within a Singularity image.

## Packages
Python scripts often require numerous packages, that have to be the correct versions, and so you need to make sure that the Singularity image or miniconda module you're running the script within has the packages required.

Located in `/home/data/NDClab/tools/containers` is the lab's current default singularity image for Python; it contains all environment variables and packages required to run a Python script.

You can identify which packages are already included in this singularity image by [logging into the hpc](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node) and using `cd` to navigate into the folder with the Python container. Activate singularity:

```
module load singularity-3.8.2
```

Then activate the interactive shell:

```
singularity shell /home/data/NDClab/tools/containers/python-3.9/python-3.9.simg
```

Lastly, request the list of installed packages with:

```
pip list
```

Alternatively, you can view the packages available in a given miniconda module by loading the module, `module load miniconda3-23.5.2`, and then running `pip list`.

If your script requires a package that is not listed here, a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html) will need to be created.


## Parallelization

To take advantage of multiple nodes on the HPC, utilize the multiprocessing module. Consult the documentation [here](https://docs.python.org/3/library/multiprocessing.html) to get started.

To quickly set up multiprocessesing functionality, you can utilize:

```python
from multiprocessing import Pool
```

...which will create a "worker" for each available CPU that you utilize.
