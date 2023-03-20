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
Located in `/home/data/NDClab/tools/containers` is the lab's current default singularity image for Python; it contains all environment variables and packages required to run a Python script.

You can identify which packages are already included in this singularity image by [logging into the hpc](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node) and using `cd` to navigate into the folder with the Python container. Activate singularity:

```
module load singularity-3.8.2
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
To run a python script using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
bash /home/data/NDClab/tools/lab-devOps/scripts/python/prun.sh <your-script-name>.py [# nodes] [hours of walltime requested]
```

By default the script will call for 1 hour of walltime (time required to execute the script) and 1 node. If walltime needed or nodes desired exceeds 1 hourand 1 node the arguments [# nodes] [hours of walltime requested] should be included (i.e. <your-script-name>.py 1 24 calls for 1 node and 24hrs walltime).

This will generate and run a Slurm script named after your script: `your-script-name.sub`. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).


## Parallelization

To take advantage of multiple nodes on the HPC, utilize the multiprocessing module. Consult the documentation [here](https://docs.python.org/3/library/multiprocessing.html) to get started.

To quickly set up multiprocessesing functionality, you can utilize:

```python
from multiprocessing import Pool
```

...which will create a "worker" for each available CPU that you utilize.
