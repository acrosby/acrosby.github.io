---
layout: post
title:  "Singularity From Local Docker Image"
categories: singularity containers
tags: ubuntu singularity docker containers HPC
---

One of the powerful features of Singularity is the ability to create Singularity images from Docker images, pulling directly from public or otherwise accessible Docker repositories. There are also some un- or minimally- documented ways to extend Singularity's impressive capacity, like converting local Docker images that may not be available in a proper Docker image repo.

To convert a local image without fetching from a remote repository you can use `docker-daemon` in the protocol as found here.

```bash
docker run --rm -ti quay.io/singularity/singularity \
    build my-test-image-output.sif docker-daemon://mytestimage:tag
```
