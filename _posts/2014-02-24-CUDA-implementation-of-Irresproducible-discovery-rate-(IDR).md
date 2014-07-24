---
layout: post
title: CUDA implementation of Irreproducible discovery rate(IDR).
---

[![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.10909.png)](http://dx.doi.org/10.5281/zenodo.10909)

Help doc on how to compile GPU(CUDA) implementation of Irreproducible Discovery Rate (IDR) analysis.

Repo link - [https://github.com/ENCODE-DCC/idr-GPU](https://github.com/ENCODE-DCC/idr-GPU)

### Prerequisites to run IDR

####Hardware requirements
* NVIDIA GPU with compute capability of 3.0 or higher
* CPU

####Software required:
* git
* cmake
* cuda (6.0 or higher)
* C++ compiler

For help installing CUDA please [click here](http://docs.nvidia.com/cuda/index.html#axzz36o8BHKsT)

### Building IDR

* Get the current repo

```
git clone --recursive https://github.com/ENCODE-DCC/idr-GPU.git
```
* Create a directory parallel to the repo (eg: build)

```
mkdir build
```
* Then follow the commands below 

```
cd build
cmake ../idr-GPU
make idr
```

### Usage

Assuming that your current working directory is the one you created. 

Eg: `build` directory from above

List all the options

 
```
./idr/idr --help
```

Sample idr run using test peak files in the repo

```
./idr/idr --peak-files ../idr-GPU/idr/data/peak1 ../idr-GPU/idr/data/peak2 --genome-file ../idr-GPU/idr/data/genome_table.txt --idr-cutoff 0.03
```

The main contributors of IDR-GPU code:

  * Nikhil R Podduturi  - nikhilrp@stanford.edu
  * J. Seth Strattan    - jseth@stanford.edu
  
J. Michael Cherry Lab, Department of Genetics, Stanford University School of Medicine