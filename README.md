# Keras-TensorFlow-GPU-Windows-Installation
10 easy steps on the installation of TensorFlow-GPU and Keras in Windows. Updated as of 2017-11-22 based on my personal experience getting things running on a GTX1080 on Windows 10.

### Step 1: Install Anaconda (latest Python 3 version) <a href="https://www.continuum.io/downloads" target="_blank">Download</a>
<p align="center"><img width=70% src="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/anaconda_windows_installation.png"></p>

### Step 2: Update Anaconda
Open Anaconda Prompt to type the following command(s)
```Command Prompt
conda update conda
conda update --all
```

### Step 3: Install CUDA Toolkit 8.0 GA2 <a href="https://developer.nvidia.com/cuda-80-ga2-download-archive" target="_blank">Download</a>
Choose your version depending on your Operating System

<p align="center"><img width=70% src="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/cuda8_windows10_local_installation.png"></p>

As of writing (2017-11-22), tensorflow-gpu==1.4.0 does not support the latest CUDA 9 yet on Windows. See https://github.com/tensorflow/tensorflow/issues/14244 for progress. Make sure you get CUDA 8.0 and (separately) cuBLAS patch 2 from the CUDA download archives at https://developer.nvidia.com/cuda-80-ga2-download-archive . 

**Be aware** that the CUDA installer's default Express settings will also install (old) video drivers and other non-CUDA-relevant software. This is part of the reason why the local installer is 1.3GB (!). I prefer the network version and I uncheck all the non-CUDA options.

### Step 4: Download cuDNN 6.0 for CUDA 8 <a href="https://developer.nvidia.com/rdp/cudnn-download" target="_blank">Download</a>
Choose your version depending on your Operating System.
Membership registration is required.

<p align="center"><img width=70% src="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/cuDNN_windows_download.png"></p>

Put your unzipped folder in C drive as follows: 
```Command Prompt
C:\cudnn-8.0-windows10-x64-v6.0
```
### Step 5: Add cuDNN into Environment PATH
Press ctrl-R, and run the command: 
```Run
sysdm.cpl
```

From here, edit your PATH variable by following these 3 steps:
<p align="center"><img width=70% src="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/CUDA_environ_variables.png"></p>

Add the following path entry in your PATH system variable.
Subjected to changes in your installation path.
```Command Prompt
C:\cudnn-8.0-windows10-x64-v6.0\cuda\bin
```

Turn off all the prompts, as they need to be restarted to use our new environment variables.

Alternatively, follow the instructions from NVIDIA in the cuDNN Install Guide. This is especially relevant if you develop in Visual Studio and want CUDA+cuDNN support there.

### Step 6: Create an Anaconda environment
Open Anaconda Prompt to type the following command(s)
```Command Prompt
conda create -n tensorflow numpy scipy matplotlib spyder
```


### Step 7: Activate the environment
Open Anaconda Prompt to type the following command(s)
```Command Prompt
activate tensorflow
```

### Step 8: Install TensorFlow-GPU (1.4.0)
Install the latest version (==1.4.0 as of 2017-11-22) in our tensorflow environment:
```Command Prompt
pip install tensorflow-gpu
```

### Step 9: Install Keras
Install the latest version of keras (==2.1.1 as of 2017-11-22) in our tensorflow environment:
```Command Prompt
pip install keras
```

### Step 10: Testing
Let's try running <a href="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/examples/mnist_mlp.py">mnist_mlp.py</a> in your prompt.

Open Anaconda Prompt to type the following command(s)
```Command Prompt
activate tensorflow
python mnist_mlp.py
```
If you get no errors: Congratulations! You have successfully run Keras (with Tensorflow backend) over GPU on Windows!

<p align="left"><img width=100% src="https://github.com/dutchminator/keras-tensorflow-windows-installation/blob/master/install_success_2.png"></p>


### Troubleshooting
If you get errors about missing .dll files, the first step is to make sure that your PATH system variable is correctly set up to point to two CUDA folders and your cuDNN folder, as shown in the screenshot in step 5. Then, make sure you have restarted your Anaconda Prompt to properly load the new PATH variable. 
Note that tensorflow-gpu is quite picky about which versions of CUDA and cuDNN are supported. At the moment of writing (2017-11-22), tensorflow-gpu==1.4.0 runs on CUDA 8.0GA2 with cuDNN v6.0. The error messages you get should reflect any version mismatches (e.g. *cudart64_7.dll* instead of *cudart64_8.dll*)
