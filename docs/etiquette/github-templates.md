---
layout: default
title: GitHub Templates
parent: Etiquette
nav_order: 2
---

### Contents

##

###




# Project Template

## Overview

The project template is a base project with all the basic functionality built in for developing
Python or R projects. This helps save time and effort at the beginning of a project and keeps
project development workflows and standards consistent across the lab. The base project uses
[Docker](https://ndclab.github.io/wiki/docs/technical-docs/docker-usage.html) as a development
platform and as a deployment platform.

By default the project contains a project directory, markdown templates for issues and pull
requests, shell scripts to automate some basic actions, and yaml configurations for [GitHub
Actions].

## Usage

To use the template first clone the project template
[repository](https://github.com/NDCLab/project-template/tree/main).

Once the repository has been cloned, open a terminal and `cd` into the directory.

Run the `init.sh` [Bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) script:

```bash
# "name" is the name of the project
# "name" should be all lower case, and contain no spaces
./init.sh name
```

To create the [Docker container](https://www.docker.com/resources/what-container), run
`docker-compose up -d --build`. This will run the [Docker Compose](https://docs.docker.com/compose/)
configuration file and automatically build the Docker container and run it.

> Note: The docker container will automatically mount the `data` and `project_name` directory. This
> will allow you to edit files under `data` and `project_name` as if you were editing them on your
> computer.

To access the container, run the command `docker exec -it project_name_app_1 /bin/bash` swapping
`project_name_app_1` for the name of the container.

> Note: To figure out the name of the docker container you can use `docker ps` to list the
> containers that are currently running. Container names are usually the name the project directory
> followed by the service name, in this case `app` and then the instance number.

The container's working directory or the directory that the user is placed in by default is
`/workspace`. In this directory, there is input and output, which are data file directories that can
contain any data and are passed from the computer running Docker and the container. In this directory,
there is also the project files, which include any Python or R script files.

In the container, `cd` to `project_name` and run either the RScript or Python script to execute the
code.

## Edit files

Any files under the `data` or `project_name` directories are accessible from either the container or
the host. That means they can be edited in the host or container using tools that the user is most
comfortable with.

On the host, navigate to the folder with the files and use a text editor or file viewer to interact
with the files.

In the container the options are more limited, by default the container does not come with a text
editor or file viewer just command line tools to manipulate the text file. It's not recommended to
use this approach as user preferences are not saved across container reboots even though files under
`project_name` and `data` persist across container reboots.

## Issues and Pull Request Templates

These templates are simple forms to help users and contributors fill out Issues and Pull Request in
a way that helps make them more readable.

Please reference the [wiki article]() that covers Issues workflow for more information.
