# Steps to install nvidia-drivers  

step 1:  
# Update your system  
sudo apt update  
sudo apt upgrade  

step 2:  
# Install required dependencies:  
sudo apt install build-essential dkms    

step 3:  
# Remove existing NVIDIA drivers and CUDA    
sudo apt-get --purge remove '*nvidia*'  
sudo apt-get --purge remove '*cuda*'  
sudo apt-get autoremove  
sudo apt-get autoclean  


step 4:  
# Add Nvidia PPa and install nvidia driver    
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt update  
sudo apt install nvidia-driver-555  

step 5:  
# Reboot the system  
sudo reboot  
# Check  
nvidia-smi  


Step 6: Install CUDA  
# do nvidia-smi and check the cuda supported version on the right top extreme  
wget https://developer.download.nvidia.com/compute/cuda/12.5.0/local_installers/cuda-repo-ubuntu2004-12-5-local_12.5.0-520.61.05-1_amd64.deb  
sudo dpkg -i cuda-repo-ubuntu2004-12-5-local_12.5.0-520.61.05-1_amd64.deb  
sudo cp /var/cuda-repo-ubuntu2004-12-5-local/cuda-*-keyring.gpg /usr/share/keyrings/  
sudo apt-get update  
sudo apt-get -y install cuda  

Step 7:
Edit ~/.bashrc  
export PATH=/usr/local/cuda-12.5/bin${PATH:+:${PATH}}  
export LD_LIBRARY_PATH=/usr/local/cuda-12.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}  

# Save changes to bashrc
source ~/.bashrc  
 

