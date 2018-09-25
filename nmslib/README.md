# nmslib

## Build docker container
> make container

## Build docker container with Jupyter
> make jupyter

## Run docker container with Jupyter
```bash
make run_notebooks NMSLIB_DIR=`pwd`/nmslib
```
## update submodule
This repo uses git submodules to simplify the pipeline scripts.

```bash
# initialize and/or sync submodules
git submodule update --init --recursive --remote nmslib
# revert any changes made locally, including those made to the submodules
git checkout --recurse-submodules -- .
```
