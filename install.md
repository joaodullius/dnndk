This is a guide on how to prepare a 16.04 LTS Ubuntu for Xilinx DNNDK 3.0

## Install NVIDIA Driver

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

## Install CUDA 9.0

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

```sudo vim /etc/environments```

Add `:/usr/local/cuda/bin` to the end of PATH=

Do `reebot`





Sources:
- https://gist.github.com/zhanwenchen/e520767a409325d9961072f666815bb8
