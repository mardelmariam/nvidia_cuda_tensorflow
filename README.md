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


## 5. Install CUDA Toolkit and cudDNN

Create an [Nvidia developer account](https://developer.nvidia.com/) if you don't have one.

Select and download the desired version numbers from [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) and [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)

For CUDA Toolkit:

* Choose your operating system as Windows. 
* Next, choose its version (If not sure, go to Control Panel | System and Security | System. It will be mentioned as its system type). 
* After that, choose any installer type. 
* When you start installation, you are prompted to select one of two installation options. Choose the "Express" one.

If the installation stops because you have a more recent Nvidia SDK installer, you might install a more recent CUDA Toolkit version.

For cuDNN:

* Click on the version you will download
* Select "cuDNN Library for Windows (x86)".
* Copy and paste cuDNN extraction files on this directory: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6


## 6. Set environment variables

On Windows, there's [a graphical procedure to view and modify environment variables](https://docs.oracle.com/en/database/oracle/machine-learning/oml4r/1.5.1/oread/creating-and-modifying-environment-variables-on-windows.html#GUID-DD6F9982-60D5-48F6-8270-A27EC53807D0).

Create CUDA_PATH if it isn't there already. Its value is Nvidia CUDA installation directory (C:\Program Files\NVIDIA GPU Computing Toolkit).

Create CUDNN as a system variable. its value is:

"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\bin;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\libnvvp;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\extras;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\include"

Replace the "X" with the version number you installed.


## 7. Sanity check: Detect Nvidia GPU for CUDA

Open Windows command window with Windows key + R, cmd. Type:

```
nvcc -V
```

Your GPU should be on the list. If not, some bugs appear. Maybe they are related to missing cuDNN files.


## 8. Install Tensorflow on Anaconda

Install [Anaconda](https://www.anaconda.com/products/individual) or your favorite tool for coding your deep learning projects.

Launch it and click on the Environments tab. Next, click on the arrow button within the base(root) entry. Click on Open Terminal. Type:

```
conda create -n tf-gpu python=3.9
```

```
conda activate tf-gpu
```

```
pip3 install tensorflow-gpu==2.6.0
```

Here, the new environment's name is tf-gpu.

Install Jupyter and pywin32:

```
pip3 install jupyter
```


Finish pywin32 installation with:

```
python [environment path]/Scripts/pywin32_postinstall.py -install
```

Your environment path should be C:/users/[windows user]/.conda/envs/tf-gpu/.

If the installation is successful, there's a message saying "The pywin32 extensions were successfully installed.". Close the command window.


## 9. Sanity check: Run Tensorflow and detect your GPU

Select tf-gpu as your environment on Anaconda. Open Terminal. Then, type:

```
python
```

```
import tensorflow as tf
```

Here, there should be no bugs.

```
print(tf.config.list_physical_devices('GPU'))
```

Your GPU is shown as:

```
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

Yay! now you may use your GPU for deep learning projects.
