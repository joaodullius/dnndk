This is a concise guide on how to prepare a 16.04 LTS Ubuntu for Xilinx DNNDK 3.0

## 1. Install NVIDIA + CUDA + cuDNN

### 1.1. Install NVIDIA Driver

My notebook has a NVIDIA 930M mobile GPU and UEFI secure boot disabled.

To install nvidia-384 (latest version of drivers in Ubuntu 16.04LTS)

```sudo apt-get install nvidia-384 nvidia-modprobe```

Do `reebot`


Check driver instalation with: 

```nvidia-smi```
```
Wed May 15 13:02:20 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.130                Driver Version: 384.130                   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce 930M        Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   48C    P8    N/A /  N/A |     91MiB /  2002MiB |     13%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1003      G   /usr/lib/xorg/Xorg                            69MiB |
|    0      1920      G   compiz                                        21MiB |
+-----------------------------------------------------------------------------+
```

### 1.2. Install CUDA 9.0

Download and install CUDA 9.0 (Nvidia Drivers + CUDA + Cuda Samples) - 1.5Gb Download
```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run
chmod +x cuda_9.0.176_384.81_linux-run
./cuda_9.0.176_384.81_linux-run --extract=$HOME
```
```
sudo ./cuda-linux.9.0.176-22781540.run
sudo ./cuda-samples.9.0.176-22781540-linux.run
sudo bash -c "echo /usr/local/cuda/lib64/ > /etc/ld.so.conf.d/cuda.conf"
sudo ldconfig
```

Edit /etc/environments with:

```sudo gedit /etc/environment```

Add `:/usr/local/cuda/bin` to the end of PATH=

Do `reebot`

```
cd /usr/local/cuda-9.0/samples
sudo make
cd /usr/local/cuda/samples/bin/x86_64/linux/release
./deviceQuery
```

Results:
```
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce 930M"
  CUDA Driver Version / Runtime Version          9.0 / 9.0
  CUDA Capability Major/Minor version number:    5.0
  Total amount of global memory:                 2003 MBytes (2100232192 bytes)
  ( 3) Multiprocessors, (128) CUDA Cores/MP:     384 CUDA Cores
  GPU Max Clock rate:                            941 MHz (0.94 GHz)
  Memory Clock rate:                             900 Mhz
  Memory Bus Width:                              64-bit
  L2 Cache Size:                                 1048576 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 1 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Supports Cooperative Kernel Launch:            No
  Supports MultiDevice Co-op Kernel Launch:      No
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.0, CUDA Runtime Version = 9.0, NumDevs = 1
Result = PASS
```
### 1.3. Install cuDNN 7.0.5 

Download cuDNN v7.0.5 (Dec 5, 2017), for CUDA 9.0 from https://developer.nvidia.com/rdp/cudnn-archive

```
sudo mv cudnn-9.0-linux-x64-v7.tgz /usr/local
cd /usr/local
sudo tar -xvzf cudnn-9.0-linux-x64-v7.tgz 
sudo ldconfig
sudo rm cudnn-9.0-linux-x64-v7.tgz 
```

# 2. Install Python 3.6
# 3. Install Anaconda
# 4. Install Tensorflow


## Sources:
For more detailed instructions please refer to:
- https://gist.github.com/zhanwenchen/e520767a409325d9961072f666815bb8
