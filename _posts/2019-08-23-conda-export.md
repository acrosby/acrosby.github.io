---
layout: post
title:  "Reproducing Conda Environments"
categories: python
tags: python linux anaconda conda env environment source package reproducible
---

This short summary is based on the Anaconda blog post here https://www.anaconda.com/moving-conda-environments/. The original blog post is a great high-level summary for the various methods in conda for reproducing environments.

* OS and platform specific (pulls from repos)
    ```
    # On source environment:
    conda list --explicit > spec-list.txt
    ```
    ```
    # New conda environment:
    conda create --name new_env_name --file spec-list.txt
    ```

* Different platforms and OS (pulls from repos, also includes `pip` installed packages)
    ```
    # On source environment:
    conda env export > env.yml
    ```
    ```
    # New conda environment:
    conda env create -f env.yml
    ```

* Platform and OS specific, no internet on target
    ```
    # On source environment:
    conda install -c conda-forge conda-pack
    conda pack -n env_name \
        -o out_name.tar.gz \
        -p /path/to/pack/
    ```
    ```
    # New conda environment:
    mkdir -p env_name
    tar -xzf out_name.tar.gz -C env_name
    source env_name/bin/activate
    conda-unpack
    ```
