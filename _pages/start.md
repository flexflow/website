---
title: Installing FlexFlow
layout: single
permalink: /start/
classes: wide
#toc: true
#toc_sticky: true
author_profile: true
header:
  overlay_image: /assets/images/header.jpg 

---
FlexFlow can be built from source code using the following instructions.


## Prerequisties
* [CUDNN](https://developer.nvidia.com/cudnn) is used to perform low-level operations.
Download and install CUDNN locally.

* [Legion](http://legion.stanford.edu) is the underlying runtime FlexFlow built on.

* [Protocol Buffer](https://github.com/protocolbuffers/protobuf) is used for representing parallelization strategies in FlexFlow.

* (Optional) [NCCL](https://github.com/NVIDIA/nccl) is used for parameter synchronization. When NCCL is not available, FlexFlow uses the Legion DMA subsystem for transferring parameters.

* (Optional) [GASNet](http://gasnet.lbl.gov) is used for multi-node executions. (see [GASNet installation instructions](http://legion.stanford.edu/gasnet))

## Build the FlexFlow Runtime

* To get started, clone the FlexFlow source code from the stable branch on github.
```
git clone -b r20.08 --recursive https://github.com/flexflow/FlexFlow.git
cd FlexFlow
```
The `FF_HOME` environment variable is used for building and running FlexFlow. You can add the following line in `~/.bashrc`.
```
export FF_HOME=/path/to/FlexFlow
```

* Build the Protocol Buffer library.
Skip this step if the Protocol Buffer library is already installed.
```
cd protobuf
./autogen.sh
./configure
make
```
* Build the NCCL library. (If using NCCL for parameter synchornization.)
```
cd nccl
make -j src.build NVCC_GENCODE="-gencode=arch=compute_XX,code=sm_XX"
```
Replace XX with the compatability of your GPU devices (e.g., 70 for Volta GPUs and 60 for Pascal GPUs).

* For users interested in using the FlexFlow C++ interface, the following command line builds a DNN model (e.g., InceptionV3).
See the [examples](https://github.com/flexflow/FlexFlow/tree/master/examples/cpp) folders for more FlexFlow applications implemented using the C++ interface.
```
./ffcompile.sh examples/cpp/InceptionV3
```

## Build the FlexFlow Keras Frontend

Alternatively, FlexFlow also support the Keras Python interface. The following instructions build the FlexFlow Python executable.

* Get the FlexFlow source code using the same instruction as above.

* Set the following enviroment variables
```
export FF_HOME=/path/to/FlexFlow
export CUDNN_DIR=/path/to/cudnn
export CUDA_DIR=/path/to/cuda
export PROTOBUF_DIR=/path/to/protobuf
export LG_RT_DIR=/path/to/Legion
```
To expedite the compilation, you can also set the `GPU_ARCH` enviroment variable.
```
export GPU_ARCH=your_gpu_arch
``` 
If Legion can not automatically detect your Python installation, you need to tell Legion manually by setting the `PYTHON_EXE`, `PYTHON_LIB` and `PYTHON_VERSION_MAJOR`, please refer to the `python/Makefile` for more details.

* Build the Flexflow python executable using the following command lines.
```
cd python
make 
```

* To run a DNN model, use the following command line.
```
./flexflow_python examples/python/keras/xxx.py -ll:py 1 -ll:gpu 1 -ll:fsize size of gpu buffer -ll:zsize size of zero buffer
``` 
