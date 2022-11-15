---
layout: default
title: MATLAB
parent: HPC
nav_order: 6
---

### Contents
1. [Packages](#packages)
2. [Running a MATLAB Script](#running-a-matlab-script)


## Packages
Installing MATLAB packages on the HPC does not involve the lab's [default containers](https://ndclab.github.io/wiki/docs/hpc/containers.html). Instead, you must manually copy all desired, supplemental scripts into your own local directory on the HPC. The steps below use installation of the MADE pipeline scripts as an example.

1. Download the [EEGLAB scripts](https://sccn.ucsd.edu/eeglab/downloadtoolbox.php) to your local machine.

2. [Log in](https://ndclab.github.io/wiki/docs/hpc/accessing.html) to the HPC and access the file navigator.

3. In your local directory, create a folder named "MATLAB" under your "Documents" folder, then click into it.

4. Use the "Upload" button to upload the entire EEGLAB folder to this new "MATLAB" folder.

5. Once upload is complete, navigate into the "plugins" folder: `~/Documents/MATLAB/eeglab/plugins`.

5. Download the following plugins using their respective links, and upload each of them to this directory:

    * [ADJUST1.1.1](https://www.nitrc.org/projects/adjust/)
    * [bids-matlab-tools](https://github.com/sccn/bids-matlab-tools)
    * [FASTER1.2.4](https://sccn.ucsd.edu/eeglab/plugin_uploader/plugin_list_all.php)


## Running a MATLAB Script
To run a script in the MATLAB programming language using the login node, log in to the [Panther Shell Access](https://ndclab.github.io/wiki/docs/hpc/accessing.html#login-node). Use `cd` to navigate to the folder that contains your script. From that location, run the following command:

```
sh /home/data/NDClab/tools/lab-devOps/scripts/matlab/rmat.sh [--parallel] <your-script-name>
```

Notes:
- `<your-script-name>` is the name of your ".m" file, but without the file extension
- you can optionally attached the `--parallel` flag to specify that this job requires parallel processing

This will generate an Slurm script named after your script: `your-script-name.sub`. Run this file [as you would any Slurm script](https://ndclab.github.io/wiki/docs/hpc/jobs.html#running-a-slurm-file).