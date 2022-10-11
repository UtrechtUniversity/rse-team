# Deep learning on Research Cloud

Surf Research Cloud provides powerful Virtual machines that can be configured with 1 or multiple GPU devices to run e.g. Deep learning models. Below are some notes for setting up a Pytorch based and Tensorflow based deep learning environment using miniconda. Research cloud currently provides Ubuntu workspaces with CUDA 11 preinstalled (name e.g.: "Ubuntu 18.04 with CUDA"). We also provide Ubuntu workspaces with Miniconda and Cuda installed (available upon request). Start the workspace and log in using SSH before running the steps:

## Step 1: Install Miniconda (if necessary)

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
After this, `logout`, and log back in via SSH for the changes to take effect.


## Step 2: Create a Conda environment

Create a conda environment, where `my_env` in the command below can be changed to a more informative name:
```
conda create --name my_env python=3.9
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
python3.9
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

## Running Jupyter notebooks

To run Jupyter notebooks in this deep learning environment, install jupyter first:

```
conda install -c conda-forge jupyter
```
Since a headless Ubuntu machine is not equipped with a web browser, you will have to connect to the web interface of the remote server in order to access the notebooks from your local internet browser. To do this, logout and log back in via SSH and use SSH tunneling to connect to the jupyter web interface:
```
logout
```
```
ssh -L 8888:localhost:8888 your_server_username@your_server_ip
```
Now reactivate your environment and start jupyter:
```
source activate my_env
jupyter notebook
```

The output will look similar to this:

```
[C 19:46:22.367 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=Example_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675&tokenExample_Jupyter_Token_3cadb8b8b7005d9a46ca4d6675
```

The token that is printed here is needed later on to login to jupyter.

In your local internet browser, go to this address:
```
http://localhost:8888
```

Now copy the token that is visible in the ssh session and paste it here.

To install new python libraries in your environment while running the jupyter notebooks, start another ssh session, activate the conda environment and install the required libraries. 

Further reading: [How to install run and connect to jupyter on a remote server](https://www.digitalocean.com/community/tutorials/how-to-install-run-connect-to-jupyter-notebook-on-remote-server)
