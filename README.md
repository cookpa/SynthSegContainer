# SynthSegContainer

Containerized [SynthSeg](https://github.com/BBillot/SynthSeg).

## Building with docker

Before building, download the models as instructed in step 3 of the [SynthSeg
installation instructions](https://github.com/BBillot/SynthSeg#installation) and place
them in `synthseg_models/`.

Then, build with one of the available Dockerfiles.

## Dockerfile.cuda

This file uses a PPA from the "deadsnakes" group, because the official
Ubuntu packages for python3.8 lead to errors with the dependencies.

The base image provides CUDA 10.1 and cuDNN 7.0. The SynthSeg page says to use Cuda
10.0, but that did not work for me.


## Dockerfile.cpu

This uses a smaller base image with official Python 3.8 and without CUDA, for users that
don't need to run on the GPU.


# Dockerfile.tfsrc

This builds without CUDA, but enhances CPU performance by building tensorflow from source.
This takes longer and by default optimizes the tensorflow binary for "native"
architecture. This is customizable by changing the configuration options in
`tf_configure.bazelrc.in`.

Natively optimized tensorflow operations are much faster, for SynthSeg the speedup is
about 4x on a new Intel i7 CPU. But it does make the container less portable.


## Usage

The entrypoint to the container is the SynthSeg prediction script
`SynthSeg_predict.py`. Run without args to see usage.


## Docker containers

Available on
[DockerHub](https://hub.docker.com/repository/docker/cookpa/synthseg/general).


## Singularity

For GPU support, build from synthseg:cuda-latest and run with `singularity --nv`.
This has been tested on Singularity 3.8.4, it may not work with older versions.


## Licensing and citations

[SynthSeg license](https://github.com/BBillot/SynthSeg/blob/master/LICENSE.txt).

The authors ask that if it is used in published research, to cite:

SynthSeg: Domain Randomisation for Segmentation of Brain MRI Scans of any
Contrast and Resolution
B. Billot, D.N. Greve, O. Puonti, A. Thielscher, K. Van Leemput, B. Fischl, A.V.
Dalca, J.E. Iglesias [arxiv](https://arxiv.org/abs/2107.09559)

For cortical parcellation, automated QC, or robust fitting, please cite the following paper:

Robust Segmentation of Brain MRI in the Wild with Hierarchical CNNs and no Retraining
B. Billot, M. Colin, S.E. Arnold, S. Das, J.E. Iglesias [MICCAI
2022](https://link.springer.com/chapter/10.1007/978-3-031-16443-9_52)
