1. What is CUDA?
   CUDA is a parallel computing platform and programming model that makes using a GPU for general purpose computing simple.
   The CUDA platform is a software layer that gives direct access to the GPU's virtual instruction set and parallel computational elements, for the execution of compute kernels
   
2. What is CUDNN?
   The NVIDIA CUDA® Deep Neural Network library (cuDNN) is a GPU-accelerated library of primitives for deep neural networks. cuDNN provides highly tuned implementations for standard routines such as forward and backward convolution, pooling, normalization, and activation layers.
   Built on CUDA
    
3. What is CUDA Toolkit? (installs Driver and CUDA)
   The toolkit includes GPU-accelerated libraries, debugging and optimization tools, a C/C++ compiler and a runtime library 
    
driver version - 
 cat /proc/driver/nvidia/version
 nvidia-smi
 
cuda version -
 cat /usr/local/cuda/version.txt
 nvidia-smi
 
cudnn version 
nvcc --version

Download links:
https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux
https://developer.nvidia.com/rdp/cudnn-download

Official documentation:
https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installdriver


sudo service lightdm stop # or pkill Xorg

install cuda toolkit 
install cudnn

sudo modprobe -r nvidia
sudo modprobe nvidia

sudo service lightdm start


## Nvidia-Docker

! Only the driver must be installed on the host. The CUDA version from the container must be compatible with the host driver.

sudo apt-get install nvidia-container-toolkit
