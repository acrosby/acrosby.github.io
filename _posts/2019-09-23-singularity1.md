---
layout: post
title:  "Singularity Container System for HPC"
categories: ubuntu, singularity, docker, containers, HPC, WRF
tags: ubuntu, singularity, docker, containers, HPC, WRF
---

At work I had a task to port the WRFv4 atmospheric model that we currently run in the office, from a Docker container, up to the Lonestar5 (LS5) supercomputer at the Texas Advanced Computing Center (TACC). My first impulse was to simply replicate the Dockerfile steps that we use in a simple bash script to natively build the required WRF executables.

Since I always forget the `module load` commands, I opened up the LS5 documentation. In doing so, I noticed that a recent update system update provides support for ["Singularity"](https://sylabs.io/singularity/) containers. Somehow I missed the rising popularity and support for Singularity, but was intrigued because it attempts to solve several of the problems we deal with running parallel numerical models (MPI, GPU and queue/batch systems) with Docker containers. And so I went down the rabbit hole of researching and installing Singularity with the hopes of replicating our Docker-like container workflows in a way that will run on LS5.

## Installation

I ran the following steps on my Ubuntu 18.04 workstation to install Singularity based on the instructions found [here](https://github.com/sylabs/singularity/blob/master/INSTALL.md).

```bash
sudo apt-get update && \
  sudo apt-get install -y build-essential \
  libssl-dev uuid-dev libgpgme11-dev libseccomp-dev \
  pkg-config squashfs-tools cryptsetup

```

I originally attempted to use my system installed GO version, but apparently install requires 1.11+. The following will install 1.12.6 from Google.

```bash
export VERSION=1.12.6 OS=linux ARCH=amd64
wget -O /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz https://dl.google.com/go/go${VERSION}.${OS}-${ARCH}.tar.gz && \
  sudo tar -C /usr/local -xzf /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz
```

Setup some environment vars that are used later on.

```bash
echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
  echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
  source ~/.bashrc
```

Download git repo for Singularity and build tagged version `3.3.0-rc.4`, which was the most [recent](https://github.com/sylabs/singularity/tags) at the time:

```bash
mkdir -p ${GOPATH}/src/github.com/sylabs && \
  cd ${GOPATH}/src/github.com/sylabs && \
  git clone https://github.com/sylabs/singularity.git && \
  cd singularity

git checkout v3.3.0-rc.4

cd ${GOPATH}/src/github.com/sylabs/singularity && \
  ./mconfig && \
  cd ./builddir && \
  make && \
  sudo make install
```

Check that it built correctly:

```bash
singularity version
```

## Hello-world

Singularity uses a file defining the containerized environment and application called a definition file, which is analogous to a Dockerfile however the syntax is different. A comparison between the two can be found [here](https://sylabs.io/guides/3.3/user-guide/singularity_and_docker.html#sec-deffile-vs-dockerfile).

### Definition Files

The header configures the base image to start from, and the sections that follow configure the environment for our specific use.

The following definition file uses a base Ubuntu 18.04 LTS images as the starting point, and then just updates apt-get repository. When the container runs it will `echo "Hello World!"`.

```yaml
BootStrap: library
From: ubuntu:18.04

%post
    apt-get -y update

%runscript
    echo "Hello World!"
```

Sections that might be necessary to build an image include:

* `%post` - Commands that are run on top of the base image OS at build time.
* `%environment` - Allows you to prove environment variables.
* `%runscript` - Defines what runs when the container is executed.
* `%labels` - Allows you to provide custom metadata.

For more information see the definition file [documentation](https://sylabs.io/guides/3.3/user-guide/definition_files.html#definitionfiles).

### Example build and run

I can build and run the container like:

```bash
# singularity build <OUTPUT IMAGE> <DEF FILE>
sudo singularity build hello-world.sif hello-world.def
./hello-world.sif
```

Output:
```
Hello World!
```

## Building from Docker

It would be relatively straight forward to just transpose the syntax of my existing WRF Dockerfile to the syntax expected by Singularity, but it seems that Singularity supports Docker Hub and Docker images themselves. In fact, Singularity can convert and run images directly from Docker Hub or a local hub.

### Run straight from docker repository

I can run `adcprep` for the ADCIRC model, which we have as a Docker image in a local repository, on-the-fly with the following:
```bash
SINGULARITY_NOHTTPS=1 singularity exec docker://our.repo:port/oceanwx/adcswan:arc_nws13 adcprep
```

### Build Singularity SIF image from repository

With the following command, I can pull our WRFv4 Docker images out of our local repository and convert it directly to Singularity's SIF image format.

```bash
export SINGULARITY_NOHTTPS=1
singularity build \
    wrf-4.0.2-intel.sif \
    docker://our.repo:port/oceanwx/wrf:4.0.2
```

```
INFO:    Starting build...
Getting image source signatures
...
Writing manifest to image destination
Storing signatures
INFO:    Creating SIF file...
INFO:    Build complete: wrf-4.0.2.sif
```

There is still some more [work](https://sylabs.io/guides/3.3/user-guide/mpi.html) to be done to ensure that my WRF's MPI implementation will work correctly with the cluster's implementation on LS5, but since both are using Intel's versions I am crossing my fingers.

---
Further reading:

* https://sylabs.io/singularity/
* https://sylabs.io/guides/3.3/user-guide/
* https://singularity-tutorial.github.io/
* https://sylabs.io/guides/3.3/user-guide/mpi.html
* https://sylabs.io/guides/3.3/user-guide/definition_files.html#definitionfiles
* https://sylabs.io/guides/3.3/user-guide/singularity_and_docker.html#sec-deffile-vs-dockerfile
* https://github.com/sylabs/singularity/blob/master/INSTALL.md
* https://github.com/sylabs/singularity/issues/1537

Singularity Citation:

1. Kurtzer GM, Sochat V, Bauer MW (2017) Singularity: Scientific containers for mobility of compute. PLoS ONE 12(5): e0177459. https://doi.org/10.1371/journal.pone.0177459
2. Kurtzer, Gregory M.. (2016). Singularity 2.1.2 - Linux application and environment
containers for science. https://doi.org/10.5281/zenodo.60736
