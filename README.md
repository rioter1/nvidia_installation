# Steps to install nvidia-drivers  

# step 1: Update your system  
sudo apt update  
sudo apt upgrade  

# step 2: Install required dependencies:  
sudo apt install build-essential dkms    

# step 3: Remove existing NVIDIA drivers and CUDA    
sudo apt-get --purge remove '*nvidia*'  
sudo apt-get --purge remove '*cuda*'  
sudo apt-get autoremove  
sudo apt-get autoclean  


# step 4: Add Nvidia PPa and install nvidia driver    
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt update  
sudo apt install nvidia-driver-555  

# step 5:  Reboot the system  
sudo reboot  
# and check
nvidia-smi  


# Step 6: Install CUDA  
# do nvidia-smi and check the cuda supported version on the right top extreme  
wget https://developer.download.nvidia.com/compute/cuda/12.5.0/local_installers/cuda-repo-ubuntu2004-12-5-local_12.5.0-520.61.05-1_amd64.deb  
sudo dpkg -i cuda-repo-ubuntu2004-12-5-local_12.5.0-520.61.05-1_amd64.deb  
sudo cp /var/cuda-repo-ubuntu2004-12-5-local/cuda-*-keyring.gpg /usr/share/keyrings/  
sudo apt-get update  
sudo apt-get -y install cuda  

sudo apt-get install -y cuda-drivers-555  

# Step 7: Edit ~/.bashrc  
export PATH=/usr/local/cuda-12.5/bin${PATH:+:${PATH}}  
export LD_LIBRARY_PATH=/usr/local/cuda-12.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}  

# Save changes to bashrc
source ~/.bashrc  

# Step 8: Install CUDNN

# Download Cudnn package from https://developer.nvidia.com/cudnn-downloads according to your system configuration  

sudo dpkg -i cudnn-local-repo-$distro-9.x.y_1.0-1_$architecture.deb  
sudo cp /var/cudnn-local-*/cudnn-*-keyring.gpg /usr/share/keyrings/  
sudo apt-get update  
sudo apt-get -y install cudnn9-cuda-12  

locate /cudnn_samples_v9/mnistCUDNN (mine was stored in /usr/src/cudnn_samples)  
cd /usr/src/cudnn_samples_v9/mnistCUDNN  

# install dependencies
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev  
sudo apt-get install libfreeimage3 libfreeimage-dev  

# execute
sudo make clean  
sudo make  

Result should be TEST PASSED!  


# Even after installation there is a chance that cudnn, cuda might not interact with each other, the .so files might not be saved or created in /usr/local/cuda-12.5/lib64 folder
# Check if the so files exist in the lib64 folder. 

ls /usr/local/cuda-12.5/lib64/libcudart.so*  
ls /usr/local/cuda-12.5/lib64/libcublas.so*  
ls /usr/local/cuda-12.5/lib64/libcublasLt.so*  
ls /usr/local/cuda-12.5/lib64/libcufft.so*  
ls /usr/local/cuda-12.5/lib64/libcusparse.so*  
ls /usr/local/cuda-12.5/lib64/libcudnn.so*  

# in case the files do not exist, locate them

locate "filepath"  

# when you find the file, create a symlink in the lib64 folder
sudo ln -s /home/antpc/anaconda3/lib/python3.9/site-packages/nvidia/cudnn/lib/libcudnn.so.8 /usr/local/cuda-12.5/lib64/libcudnn.so.8  

# While installing softwares like tensorflow, it is very important to first check whether the installed software is interacting with GPU. 
Before installing tensorflow, go to https://www.tensorflow.org/install/source?hl=en#gpu and check which version of tensorflow is compatible with installed cuda and cudnn version  
pip install tensorflow==2.15.0 (this will install gpu version)   
python  
import tensorflow as tf  
print("Num of GPUs available: ", len(tf.test.gpu_device_name()))  
