---
layout: post
title:  "Running WRF Singularity Container on TACC Systems"
categories: ubuntu, singularity, docker, containers, HPC, WRF
tags: ubuntu, singularity, docker, containers, HPC, WRF, TACC
---


So prior the the recent TACC training on containers I was trying to get our WRF Docker images to run up on the TACC HPC infrastructure using Singularity.

I checked the version of Singularity on the Lonestar5 cluster and it was behind the most recent versions a bit, but luckily there are Docker images for Singularity so you can play with whatever version might be required. (The version on Lonestar5 may already be updated by now too, recent version on Stampede2 was 3.4.3.)

Check TACC system Singularity version:

```
module spider tacc-singularity
module load tacc-singularity
singularity --version
```

Locally pull a specific version of Singularity:

```
docker pull singularityware/singularity:2.6
```

Build Singularity image file (sif) from Docker image accessible from a Docker repository (in my case a recent version of WRF that I have in a Docker image already):

```
docker run --rm -ti -e SINGULARITY_NOHTTPS=1 \
  -v /home/alex/Temp:/home/alex/Temp singularityware/singularity:2.6 \
      build /home/alex/Temp/wrf-4.0.2-intel_260.sif \
      docker://repository:port/oceanwx/wrf:4.0.2-intel
```

## MPI is tricky

Unfortunately, Lonestar5 is using a custom Cray implementation of MPI which is not really compatible with any implementation we have access to already--so I can't just upload any of my existing images to LS5.

TACC *does* provide base Docker images that contain the appropriate dependencies including MPI for their other HPC systems, however. Information about these can be found here: [https://github.com/TACC/tacc-containers](https://github.com/TACC/tacc-containers)

And the Docker images available on DockerHub are here: [https://hub.docker.com/u/tacc](https://hub.docker.com/u/tacc)

Using one of these in a Dockerfile (designed to run on Stampede2 with MPI) is as simple as

```dockerfile
FROM tacc/tacc-ubuntu18-mvapich2.3-psm2:0.0.2
...
```
at the start of a Dockerfile rather than a base Ubuntu Linux image. There are base images based on other versions and flavors of Linux as well.

## More Containers at TACC Documentation (from their training)

* [https://github.com/TACC/containers_at_tacc](https://github.com/TACC/containers_at_tacc)
* [https://containers-at-tacc.readthedocs.io/en/latest/](https://containers-at-tacc.readthedocs.io/en/latest/)

The MPI and GPU sections specifically:

[https://containers-at-tacc.readthedocs.io/en/latest/singularity/03.mpi_and_gpus.html](https://containers-at-tacc.readthedocs.io/en/latest/singularity/03.mpi_and_gpus.html)
