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

Create an [Nvidia developer account](https://developer.nvidia.com/) if you don't have one.

Select and download the desired version numbers from [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) and [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)

For CUDA Toolkit:

Choose your operating system as Windows. Next, choose its version (to know your system's architecture, go to Control Panel | System and Security | System. It will be mentioned as its system type). 
After that, choose any installer type. When you start installation, you are prompted for select one of two installation options. Choose the "Express" one.

For cuDNN:

Click on the version you will download, and select "cuDNN Library for Windows (x86)".

Install CUDA Toolkit. Copy and paste cuDNN extraction files on this directory: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6


## 6. Set environment variables

On Windows, there's [a graphical procedure to view and modify environment variables](https://docs.oracle.com/en/database/oracle/machine-learning/oml4r/1.5.1/oread/creating-and-modifying-environment-variables-on-windows.html#GUID-DD6F9982-60D5-48F6-8270-A27EC53807D0).

Create CUDA_PATH if it doesn't appear as a system variable. Its value is Nvidia CUDA installation directory (C:\Program Files\NVIDIA GPU Computing Toolkit).

Create CUDNN as a system variable. its value is:

"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\bin;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\libnvvp;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\extras;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\include"

Replace the "X" with the version number you installed.


## 7. Sanity check: Detect Nvidia GPU

Open Windows command window with Windows key + R, cmd. Type:

```
nvcc -V
```




## ?. Bugs and solutions

You have a more recent Nvidia SDK installer: Install a more recent CUDA Toolkit version.
