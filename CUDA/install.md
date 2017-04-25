cd ~/Install/CUDA
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run
md5sum cuda_8.0.61_375.26_linux-run
lsmod | grep nouveau
sudo vim /usr/lib/modprobe.d/blacklist-nouveau.conf
     blacklist nouveau
     options nouveau modeset=
reboot
sudo init 3
(CTRL+ALT+F1) and then login
cd Install/CUDA
sudo sh cuda_8.0.61_375.26_linux-run
(answer yes to everything)
reboot
sudo vim /etc/bash.bashrc
     # cuda path
     export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
     export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
sudo chown -R root NVIDIA_CUDA-8.0_Samples/
mv NVIDIA_CUDA-8.0_Samples/ /usr/local/cuda-8.0/
cd /usr/local/cuda-8.0/NVIDIA_CUDA-8.0_Samples/
sudo apt-get install build-essential
sudo make
bin/x86_64/linux/release/deviceQuery
cd ~/Install/CUDA
Get an NVIDIA account log on and download the cudnn tarball
wget https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v5.1/prod_20161129/8.0/cudnn-8.0-linux-x64-v5.1-tgz
tar -xvf cudnn-8.0-linux-x64-v5.1.tgz
sudo chown -R root cuda
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-8.0/include/
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64/
tensorflow 2.7 (anaconda)
conda create -n tf27 pip
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp27-none-linux_x86_64.whl
tensorflow 3.5 (anaconda)
conda create -n tf35 pip
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp35-cp35m-linux_x86_64.whl
