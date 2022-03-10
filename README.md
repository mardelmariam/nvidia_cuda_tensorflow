# nvidia_cuda_tensorflow
How to use your Nvidia GPU on Windows with Tensorflow, for deep learning

## 1. Check that your GPU is CUDA-capable

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

Choose your operating system as Windows. Next, choose its version (to know your system's architecture, go to Control Panel | System and Security | System. It will be mentioned as its system type). Next, choose any installer type. When you start installation, you are prompted for select one of two installation options. Choose the "Express" one.

Install CUDA Toolkit. After finishing, copy and paste cuDNN extraction files 


## 6. Set environment variables

Create CUDA_PATH. It should point to the Nvidia CUDA installation directory (C:\Program Files\NVIDIA GPU Computing Toolkit).

Create CUDNN. It should point to these folders:

- C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\bin
- C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\libnvvp
- C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\extras
- C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\include

Replace the "X" with the version number you installed.


## 7. Sanity check: Detected Nvidia GPU by CUDA applications


## ?. Bugs and solutions

You have a more recent Nvidia SDK installer: Install a more recent CUDA Toolkit version.
