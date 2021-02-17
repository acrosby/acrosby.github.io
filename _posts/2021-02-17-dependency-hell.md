---
layout: post
title:  "Dependency Hell"
categories: python
tags: python linux anaconda conda env environment source package reproducible pip xarray netcdf
---

I started my Python package management journey years ago using `pip`, then more recently I embraced Anaconda and `conda` more fully (particularly with the "conda-forge" repository) to resolve complex dependencies along with system/binary dependencies. Recently, when attempting to update our team's standard Python docker image with the latest versions of the packages we use, and include some new ones, it appears that relying on `conda` and conda-forge is untenable: I have been unable to resolve the appropriate set of versions for the scientific Python packages our team require for our work. I have moved back to `pip` for packages which are not provided in the default Anaconda repository. `pip` has and continues to make a number of improvements, and had no problem providing our extra dependencies.

I suspect there is some over-specifying of version requirements going on in conda-forge, failure to maintain the conda-forge package requirements, and/or out-of-date sets of standard binary dependencies on conda-forge. Whatever the cause, this really hampers my use of `conda` for package management, since many of the packages we need are not available in the default Anaconda repo. So far, it's `pip` to the rescue...
