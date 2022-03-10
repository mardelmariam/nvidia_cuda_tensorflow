# nvidia_cuda_tensorflow
How to use your Nvidia GPU on Windows 10 with Tensorflow, for deep learning

## 1. Check that your GPU is capable of using CUDA

If you have an Nvidia GPU that is listed on [Nvidia CUDA support matrix](https://developer.nvidia.com/cuda-gpus), then your GPU is capable of running CUDA applications.

## 2. Install Visual Studio with Nvidia integrations

Download and install:

* Microsoft Visual Studio 2017 Community Edition
* Microsoft Visual Studio 2019 Community Edition

From [My Visual Studio Portal](https://my.visualstudio.com/Downloads).

For both versions, you need to install two components:

* Desktop development with .NET
* Desktop development with C++

## 3. Install Nvidia Nsight Integration

Fron Visual Studio's main menu, select:

* Tools | Extensions and Updates (VS 2017)
* Extensions | Manage Extension (VS 2019)

Expand Online, and search for "Nsight integration". Nvidia Nsight Integration should be available for update or download and install.


## 4. Check the most recent Tensorflow version you may use with your GPU

Check [Tensorflow's table of tested versions](https://www.tensorflow.org/install/source#gpu). The version you choose points the Python, CUDA and cuDNN versions you should install.


## 5. Download CUDA Toolkit and cudDNN

Select and download the desired version numbers from [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) and [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)
