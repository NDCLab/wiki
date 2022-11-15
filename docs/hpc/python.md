---
layout: default
title: Python
parent: HPC
nav_order: 7
---

### Contents
1. [Packages](#packages)
2. [Running a Python Script](#running-a-python-script)
3. [Parallelization](#parallelization)


## Packages
Located in `/home/data/NDClab/tools/containers` is the lab's current default singularity image for Python; it contains all environment variables and packages required to run any Python script.

You can identify which packages are already included in this singularity image by [logging into the hpc](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node) and using `cd` to navigate into the folder with the Python container. Activate singularity:

```
module load singularity-3.5.3
```

Then activate the interactive shell:

```
singularity shell container.simg
```

Lastly, request the list of installed packages with:

```
pip list
```

If your script requires a package that is not listed here, a [new container](https://ndclab.github.io/wiki/docs/hpc/containers.html) will need to be created.


## Running a Python Script
To run a script in the R programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
sh /home/data/NDClab/tools/lab-devOps/scripts/python/prun.sh <your-script-name>.py
```

This will generate an Slurm script named after your script: `your-script-name.sub`. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).


## Parallelization

To take advantage of multiple nodes on the HPC, utilize the multiprocessing module. Consult the documentation [here](https://docs.python.org/3/library/multiprocessing.html) to get started.

To quickly set up multiprocessesing functionality, you can utilize:

```python
from multiprocessing import Pool
```

...which will create a "worker" for each available CPU that you utilize.
