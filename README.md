# Nvidia-GPU-driver-installation
GPU CUDA toolkit
## Installation on Ubuntu 18.04
1. Ensure presense of Nvidia CUDA-Enabled GPU
```
lspci | grep -i nvidia
```
2. Install required apt dependencies
```
sudo apt-get install build-essentials gcc-multilib dkms -y
```
3. Disabling Nouveau driver
```
Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following contents:
blacklist nouveau
options nouveau modeset=0

Regenerate the kernel initramfs:
$ sudo update-initramfs -u
$ reboot
```
4. Perform CUDA Toolkit installation
```
$ sudo ./cuda_10.1.105_418.39 --tmpdir=/home (for non executable directory for /tmp)
```
5. Install libcudnn and libnvdia-container toolkit
```
sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb libcudnn7-dev_7.6.5.32-1+cuda10.1_amd64.deb
sudo dpkg -i libnvidia-container1_1.2.0-1_amd64.deb libnvdia-container-tools_1.2.0-1_amd64.deb libnvdia-container-toolkit_1.2.0-1_amd64.deb
```
6. Post installation Steps
```
$ vi ~/.bashrc
Append 
#CUDA
export PATH=/user/local/cuda-10.1/bin${PATH:+${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64
```
7. To Remove
```
To remove CUDA Toolkit:
$ sudo apt-get --purge remove "*cublas*" "*cufft*" "*curand*" \
 "*cusolver*" "*cusparse*" "*npp*" "*nvjpeg*" "cuda*" "nsight*" 
To remove NVIDIA Drivers:
$ sudo apt-get --purge remove "*nvidia*"
```
