# nvidia_cuda_tensorflow
This is a guide of how to use your Nvidia GPU on Windows with Tensorflow, for deep learning.
Although Linux is the best OS for Deep Learning, it's worth having some Python local venvs in Windows for smaller models!

This tutorial should also be of great help to those who have older GPUs.

## 1. Check that your GPU is CUDA-capable

If you have an Nvidia GPU that is listed on [Nvidia CUDA support matrix](https://developer.nvidia.com/cuda-gpus), then your GPU is capable of running CUDA applications.

## 2. Install Visual Studio with Nvidia integrations

Download and install:

* Microsoft Visual Studio 2017 Community Edition
* Microsoft Visual Studio 2019 Community Edition

I uploaded these files to this repo, because they don't seem to be available online anymore. 

For both versions, you need to install two components:

* Desktop development with .NET
* Desktop development with C++

## 3. Install Nvidia Nsight Integration

Fron Visual Studio's main menu, select:

* Tools | Extensions and Updates (VS 2017)
* Extensions | Manage Extension (VS 2019)

Expand Online, and search for "Nvidia N-sight integration (32 bit)". Nvidia Nsight Integration should be available for update or download and install.


## 4. Check the most recent Tensorflow version you may use with your GPU

Check [Tensorflow's table of tested versions](https://www.tensorflow.org/install/source#gpu). The version you choose points the Python, the CUDA tooklit and the cuDNN versions you should install. 

For newer GPUs, table 3 from this [NVIDIA compatibility guide](https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver) should be useful for choosing the CUDA toolkit version. Normally, a CUDA installation provides the GameReady driver kernel, so don't worry about having to install it separately. You will be good with either having or installing a driver kernel with a previous version. If you have a newer one, please uninstall it and look for another one in [NVIDIA download page](https://www.nvidia.com/download/find.aspx).

For older GPUs, please check [this page](https://www.guru3d.com/files/category/videocards-nvidia-geforce-windows-7-8-10/page-31/) if you need a driver kernel with a previous version. The table mentioned earlier is misleading. Newer versions of Nvidia's GameReady kernel drivers don't have CUDA compatibility with older GPUs. So, if you don't know which version you should install, you will need to iterate with different combinations of tensorflow, CUDA and cuDNN, each iteration with older versions (of either the CUDA toolkit, cuDNN or tensorflow), until tensorflow finally recognizes your GPU. This means that you will be repeating the following steps, so don't get discouraged: it works eventually :)

## 5. Install CUDA Toolkit and cudDNN

Create an [Nvidia developer account](https://developer.nvidia.com/) if you don't have one.

Select and download the desired version numbers from [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive) and [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)

For CUDA Toolkit:

* Choose your operating system as Windows. 
* Next, choose its version (If not sure, go to Control Panel | System and Security | System. It will be mentioned as its system type). 
* After that, choose any installer type. 
* When you start installation, you are prompted to select one of two installation options. Choose the "Express" one.

If the installation stops because you have a more recent Nvidia SDK installer, you might want to install a more recent CUDA Toolkit version.

For cuDNN:

* Click on the version you will download
* Select "cuDNN Library for Windows (x86)".
* Copy and paste cuDNN extraction files on this directory: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6


## 6. Set environment variables

On Windows, there's [a graphical procedure to view and modify environment variables](https://docs.oracle.com/en/database/oracle/machine-learning/oml4r/1.5.1/oread/creating-and-modifying-environment-variables-on-windows.html#GUID-DD6F9982-60D5-48F6-8270-A27EC53807D0).

Create CUDA_PATH if it isn't there already. Its value is Nvidia CUDA installation directory (C:\Program Files\NVIDIA GPU Computing Toolkit).

Create CUDNN as a system variable. its value is:

```
"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\bin;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\libnvvp;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\extras;C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.X\include"
```

Replace the "X" with the version number you installed.

Then, reboot your computer.


## 7. Sanity check: Detect Nvidia GPU for CUDA

Open Windows command window with Windows key + R, cmd. Type:

```
nvcc -V
```

This should show a successful compilation of NVIDIA CUDA computing modules, like this:

```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Sun_Feb_14_22:08:44_Pacific_Standard_Time_2021
Cuda compilation tools, release 11.2, V11.2.152
Build cuda_11.2.r11.2/compiler.29618528_0
```

This is optional: you can also make an additional verification process. Go to C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.X\1_Utilities\deviceQuery, and open deviceQuery_vs2019.vcxproj with Visual Studio 2019. Build this project. An executable file will be generated at C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.X\bin\win64\Debug\deviceQuery.exe

After build completion, it should report the following output:

```
========== Build: 1 succeeded, 0 failed, 0 up-t-o-date, 0 skipped ==========
```

In your command prompt, move to the folder C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.X\bin\win64\Debug and run .\deviceQuery, it will tell you whether the CUDA toolkit works. The following shows the output of my Geforce GTX 860M card.

```
.\deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GTX 860M"
  CUDA Driver Version / Runtime Version          11.2 / 11.2
  CUDA Capability Major/Minor version number:    5.0
  Total amount of global memory:                 2048 MBytes (2147483648 bytes)
  ( 5) Multiprocessors, (128) CUDA Cores/MP:     640 CUDA Cores
  GPU Max Clock rate:                            1020 MHz (1.02 GHz)
  Memory Clock rate:                             2505 Mhz
  Memory Bus Width:                              128-bit
  L2 Cache Size:                                 2097152 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total shared memory per multiprocessor:        65536 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 4 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  CUDA Device Driver Mode (TCC or WDDM):         WDDM (Windows Display Driver Model)
  Device supports Unified Addressing (UVA):      Yes
  Device supports Managed Memory:                Yes
  Device supports Compute Preemption:            No
  Supports Cooperative Kernel Launch:            No
  Supports MultiDevice Co-op Kernel Launch:      No
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 11.2, CUDA Runtime Version = 11.2, NumDevs = 1
Result = PASS
```

## 8. Creating a Python virtual environment (venv)

In your command prompt, move to the folder in which you will create a local environment for Tensorflow. Then, follow these steps:

```
python -m venv tf-gpu
cd tf-gpu/Scripts
activate
```

With the activated environment, use:

```
pip3 install tensorflow==2.X.X
```

If you are unsure of which specific sub-version of Tensorflow you will need, use a wildcard. For example, I used:

```
pip install -U "tensorflow==2.10.*"
```

After that, install Jupyter and pywin32:

```
pip3 install jupyter
```

Finish pywin32 installation with:

```
python [environment path]/Scripts/pywin32_postinstall.py -install
```

If the installation is successful, there's a message saying "The pywin32 extensions were successfully installed.". 


## 9. Sanity check: Run Tensorflow and detect your GPU

Again, in your command prompt, type:

```
python
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

Finish with:

```
exit()
```

Yay! now you may use your GPU for deep learning projects.


If you want to use more complex datasets like COCO or more complex algorithms like YOLO, follow the next steps:


## 10. Install Protocol Buffers (protobuf)

Load its [official repository](https://github.com/protocolbuffers/protobuf/releases). Look for a version that is compatible with Windows and Tensorflow.

Add the bin folder from the installation (for example, C:\protoc-21.12-win64\bin) to the PATH system variable.


## 11. Compile protos

Download [the Tensorflow models repository](https://github.com/tensorflow/models). Keep it in a good path. Execute the following command line, from the /models/research path:

```
protoc object_detection/protos/*.proto --python_out=.
```


## 12. Compile the Object Detection API

Execute its installation as:

```
cd models\research\object_detection\packages\tf2
```

If you have a relatively new GPU card, you can execute this without any issues:

```
python -m pip install .
```

If your GPU card is old, you will need to install the following packages, one by one, verifying that they remain compatible with the Tensorflow version

```
avro-python3
apache-beam
pillow
lxml
matplotlib
cython
contextlib2
six
pycocotools
scipy
pandas
tf-models-official
tensorflow_io
keras
pyparsing
sacrebleu<=2.2.0 (possible issues with newer versions)
```

If your GPU card is very old, don't worry if tf-models-official cannot be installed. You can find its source code and learn from it [separately](https://pypi.org/project/tf-models-official/2.10.0/#history). The tf-models-official repository has a folder named "official". Copy it and paste in the /models/research/ path. Ensure that you download a version that is compatible with your already installed libraries.


## 11. Create a PYTHONPATH environment variale

This variable shoud contain 3 directories: the Python environment in which Tensorflow is located, its Scripts folder, and the models/research folder. It should look like this:

```
virtual env path \ environment_name ; virtual env path \ environment_name \ Scripts ; Tensorflow models path \ models\ research
```

Now you're ready for complex computer vision projects. Have fun!


