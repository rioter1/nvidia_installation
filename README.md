Steps to install nvidia-drivers  

step 1:  
Update your system  
sudo apt update  
sudo apt upgrade  

step 2:  
Install required dependencies:  
sudo apt install build-essential dkms    

step 3:  
Remove existing NVIDIA drivers and CUDA    
sudo apt-get --purge remove '*nvidia*'  
sudo apt-get --purge remove '*cuda*'  
sudo apt-get autoremove  
sudo apt-get autoclean  


step 4:  
Add Nvidia PPa and install nvidia driver    
sudo add-apt-repository ppa:graphics-drivers/ppa  
sudo apt update  
sudo apt install nvidia-driver-525  

step 5:  
Reboot the system  
sudo reboot  
Check  
nvidia-smi  
