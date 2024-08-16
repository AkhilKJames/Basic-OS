# Learn-OS
An Operating System for a string machine. For documentation, visit [expos nitc](http://exposnitc.github.io)

## Pre-Requisite

#### Install and setup Docker on host machine

* Follow the instructions available [here](https://docs.docker.com/get-docker/) to install docker on your machine.

* You could also go through the [Docker quick start quide](https://docs.docker.com/get-started/) to know more about Docker.


## Building the container image

We'll now build the container image using the `Dockerfile`

```sh
docker build -t expos:ubuntu20.04 .
```

## Start the container instance

We'll start an instance of Container and map the local folder `workdir` into `/home/expos/workdir` directory of container.

Windows (PowerShell)
``` sh
docker run -v ${PWD}/workdir:/home/expos/myexpos/workdir -d --name expos -i expos:ubuntu20.04
```

Unix / Linux
``` sh
docker run -v $PWD/workdir:/home/expos/myexpos/workdir -d --name expos -i expos:ubuntu20.04 
```

We now have a container instance running in background with the name `expos` and required volume mounts

### Connecting to the container

We can connect to the container instance using the following commands

```sh
docker start expos # if the container instance is not already running

docker exec -it expos /bin/bash # to get a bash shell inside the container
```

After connecting to the container you can use `spl`, `expl`, `xfs-interface`, and `xsm` binaries.

If the setting up of the system is done correctly the following directories will be created.

-   **$HOME/myexpos/expl**  
    This directory contains the [ExpL](./expl.md) (Experimental Language) compiler required to compile user programs to XSM machine instructions.
  
-   **$HOME/myexpos/spl**  
    This directory contains the [SPL](./spl.md) (System Programmer's Language) Compiler required to compile system programs (i.e. operating system routines) to XSM machine instructions.
  
-   **$HOME/myexpos/xfs-interface**  
    This directory contains an interface ([XFS Interface](./xfs-interface.md) or eXperimental File System Interface) through which files from your UNIX machine can be loaded into the File System of XSM. The interface can format the disk, dump the disk data structures, load/remove files, list files, transfer data and executable files between eXpFS filesystem and the host (UNIX) file system and copy specified blocks of the XFS disk to a UNIX file.
  
-   **$HOME/myexpos/xsm**  
    This directory contains the machine simulator ([XSM](./xsm-simulator.md) or eXperimental String Machine).
  
-   **$HOME/myexpos/test**  
    This directory contains the test scripts for [eXpOS](../os-spec/index.md)
