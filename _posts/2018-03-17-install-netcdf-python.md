---
layout: post
title:  "Installing NetCDF Python Packages"
categories: netcdf python
---

I am always trying to remember how I have installed netCDF4 and related libraries for Python, and what I need to do differently for Windows systems vs. the Linux systems I usually use.

On Linux, sometimes I use the system netCDF C libaries, but often I compile and install specific versions of HDF5 and netCDF4 from scratch. Here is how I have built netCDF for various Docker container images.

```bash
# Build HDF5
cd hdf5-x.y.x
./configure --prefix=/usr/local --enable-shared --enable-hl
make
make install
cd ..

# Built NetCDF4
cd netcdf-x.y.z
LDFLAGS=-L/usr/local/lib
CPPFLAGS=-I/usr/local/include
./configure --enable-netcdf-4 --enable-dap --enable-shared --prefix=/usr/local --disable-doxygen
make
make install
cd ..

# NetCDF4 Fortran
cd netcdf-fortran-x.y.z
./configure --enable-shared --prefix=/usr/local
make
make install
cd ..
```

### netcdf4-python

I typically try to use `pip` to install Python libraries if I can. The basic NetCDF module for Python is called [`netcdf4-python`](http://github.com/unidata/netcdf4-python), but it can be installed using the name below.

```bash
pip install netcdf4
```

Many people, particularly in industry and government, have adopted Continuum Analytics' Anaconda Python distribution which includes a large set of pre-included packages and a clever package management system called `conda`. This package management system attempts to solve dependencies by up- or down-grading packages to best meet the requirements of the full set of installed packages in the distribution. Build scripts can include binary dependencies and headers that live in their own isolated environment so that they don't interfere with necessary system libraries/dependencies. I use the *conda-forge* channel to be compatible with other packages that can only be sourced there.

```bash
conda install -c conda-forge netcdf4
```

### xarray

A great package that attempts to provide a `Pandas`-like interface to multidimensional arrays that come from file formats like netCDF is xarray. A great aspect of this package is the incorporation of  `dask` to allow for out-of-core computations on these potentially large (and multi-file) arrays.

```bash
# pip
pip install xarray

# Anaconda
conda install -c conda-forge xarray
```
