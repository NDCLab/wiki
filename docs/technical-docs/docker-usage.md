---
layout: default
title: Docker Usage
parent: Technical Documentation
nav_order: 2
---
# Docker Usage

How to use `docker` to run scripts from Matlab, Python, and R-base using GUI and terminal options.

The steps are:

- Build an image,
- create a container,
- execute a script or program in the container.

## Docker CLI

Main commands for Docker are run, build, pull.

`docker run` is used to run a new container instance of an image. If the image does not exist docker
will attempt to download it from [Docker Hub](https://hub.docker.com). With run there are some
common options that you can use with it:

- `-i` or `--interactive` keeps the standard input open
- `-t` or `--tty` creates a pseudo terminal or TTY
- `--rm` removes the container when it exits; depending on how the container is configured this can
	mean onces you `exit` the terminal.

```sh
# Usage
# Will launch an Ubuntu container
# 	if it does not have the image it will download it from hub.docker.com
#		will attempt to open a tty with the bash shell
# 	and once you exit the terminal will remove (delete) the container
docker run -it --rm ubuntu /bin/bash
# After the container is created, you will be "dropped" into a bash terminal and you can
# 	run scripts with the installed interpreter.
```

`docker pull` will "pull" or download an image and all the layers required to run that image to your
computer. A normal use case for `docker pull` is to download an image you do not have by specifying
the image name; `NAME[:TAG|@DIGEST]`. `NAME` is the name of the image, for example `ubuntu`. A tag
normally refers to some form of versioning for that image, for example `ubuntu:latest`. And
`@DIGEST` refers to a specific version for that `TAG`, for example
`ubuntu@sha256:1d7b639619bd...`. Generally you specify the `TAG` and not the `DIGEST` unless you
have very specific requirements.

```sh
# Usage
docker pull ubuntu:latest
```

`docker build` will build a docker image using a `Dockerfile` or the "build instructions" for the
image. Generally you do not need additional options for the build command since most of the work is
done in the `Dockerfile`.

```sh
# Usage
docker build Dockerfile
```

Below is an example is a simple `Dockerfile` for a Python container:

```Dockerfile
FROM python:3.8

# Create the working dir
WORKDIR /python_wdir

# Install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy python source files into the image
COPY src/ .
```

### Additional Resources

If you are using the CLI, the best resource available as reference is the help text, you can access
it by doing `docker --help` or `docker command --help`. Alternatively for a more in-depth
explanations for commands and options access the manual pages via `man docker` or
[online](http://manpages.org/docker)

[Wiki article](https://wiki.archlinux.org/index.php/Docker)

## Docker Compose

Docker Compose is a way to simplify the build and deploy step for docker containers. It will handle
most things like creating and removing a container, mounting and unmounting directories (folders),
and creating and deleting networks. Its usage is very simple in most cases; you either run
`docker-compose up -d` to start the docker container in a detached state or `docker-compose down` to
stop the container and clean up any resources that were left dangling.

The more time consuming step is creating the configuration file to define the container stack, this
stack can have one or many container definitions. Here is a simple example for python:

```yaml
version: 3
services:
  app:
    build: .
      volumes:
        - "./data/:/data_in_container"
```

### Additional Resources

For a full overview of options reference the [Compose file
specification](https://docs.docker.com/compose/compose-file/). There are 15 versions of the format,
as a rule of thumb use version 3.0 and only bump the minor version, 3.x, when you need specific
functionality or something seems to not work as intended.