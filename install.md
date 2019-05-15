This is a guide on how to prepare a 16.04 LTS Ubuntu for Xilinx DNNDK 3.0

## Install NVIDIA Driver

My notebook has a NVIDIA 930M mobile GPU and UEFI secure boot disabled.

To install nvidia-384 (latest version of drivers in Ubuntu 16.04LTS)

```sudo apt-get install nvidia-384 nvidia-modprobe```

Reboot.


Check driver instalation with ```nvidia-smi```



Sources:
- https://gist.github.com/zhanwenchen/e520767a409325d9961072f666815bb8
