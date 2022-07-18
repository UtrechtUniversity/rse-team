# Deep learning on Research Cloud

Surf Research Cloud provides powerful Virtual machines that can be configured with 1 or multiple GPU devices to run e.g. Deep learning models. Below are some notes for setting up a Pytorch based and Tensorflow based deep learning environment using miniconda. Research cloud currently provides Ubuntu 18.04 workspaces with CUDA 11 preinstalled (name: "Ubuntu 18.04 with CUDA"). Start the workspace and log in using SSH before running the steps:

## Step 1: Install Miniconda

Download the latest installation shell script:
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Make the miniconda installation script executable:
```
chmod +x Miniconda3-latest-Linux-x86_64.sh
```

Run the miniconda installation script:

```
./Miniconda3-latest-Linux-x86_64.sh
```

## Step 2: Create a Conda environment

Create a conda environment, where `my_env` in the command below can be changed to a more informative name:
```
conda create --name my_env python=3.7
```
Activate the environment:
```
conda activate my_env
```

## Step 3a: Install Cuda toolkit and Pytorch libraries

Run this command to install all required libraries:
```
conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
```
To test, start python:
```
python3.7
```
Within python run the following commands, and if all went correct the output should be similar:

```
>>> import torch
>>> torch.cuda.is_available()
True

>>> torch.cuda.device_count()
1

>>> torch.cuda.current_device()
0

>>> torch.cuda.device(0)
<torch.cuda.device at 0x7efce0b03be0>

>>> torch.cuda.get_device_name(0)
'GeForce GTX 950M'
```

## Step 3b: Install Cuda toolkit and Tensorflow

Run these command to install all required libraries:
```
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0
python3 -m pip install tensorflow
```
To test, run:
```
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```


