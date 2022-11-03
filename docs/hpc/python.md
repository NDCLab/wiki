---
layout: default
title: Python
parent: HPC
nav_order: 7
---

### Contents
1. [Packages](#packages)
2. [Running a Python Script](#running-a-python-script)
3. [GUI](#gui)


## Packages
Located in `/home/data/NDClab/tools/` is the lab's current default singularity image for Python; it contains all environment variables and packages required to run any Python script.

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
TBD


## GUI
TBD