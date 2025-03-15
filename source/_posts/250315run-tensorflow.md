---
title: 和科研中无人问津的TensorFlow斗智斗勇 --配置tensorflow环境
tags:
  - TensorFlow
  - docker
  - gpu
categories:
  - 教程
excerpt: >-
  tensorflow是google开源的深度学习框架，但是在科研中并不主流，其文档及环境配置也不如torch方便。并且其对本机环境的依赖性很强，而我又不想在本机上安装cuda（因为会与其他torch环境有冲突）
date: 2025-03-15 16:53:25
---


为了运行[sionna](https://nvlabs.github.io/sionna/)，一个nvidia开发的无线信道仿真工具，依赖于tensorflow
# tensorflow官方的安装要求
[官网](https://www.tensorflow.org/install/gpu)上给出了tensorflow的安装要求，其中包括了cuda，cudnn等环境的要求，这些环境的安装对于初学者来说是一个很大的挑战，而且这些环境对于不同的深度学习框架来说是有冲突的，所以我不想在本机上安装这些环境，而是选择在docker中安装tensorflow环境。

# conda安装tensorflow环境
正如摘要中提到的，我不想在本机配置cuda-toolkit, cudnn等环境，在一开始我尝试按照pytorch类似的方法在conda中安装cuda，但因为对tensorflow的不熟悉，且官方文档对于各个版本tensorflow对应的cuda版本等信息不够清晰，尝试了几种不同的组合，好像中间成功过（但因为我代码有个地方有bug，所以程序没运行成功，并且tensorflow也有Error报错，令我误以为是环境没有配置好）

报错如下：
```
E tensorflow/compiler/xla/stream executor/cuda/cuda dnn.cc:9342]
Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
E tensorflow/compiler/xla/stream executor/cuda/cuda fft.cc:609] Unable to register cuFfT factor/: Attempting to reaister factory for plugin cuFFT when one has already been reaistered
E tensorflow/compiler/xla/stream executor/cuda/cuda blas,cc:1518l Unable to reaister cuBLAs factory: Attempting to register factory for plugin cuBLAs when one has already been registered
```

根据在github上讨论，这个error更像是warning，不影响程序的运行，后续有时间我再补充上使用conda配置tensorflow的方法

关键的思路就是使用conda安装cuda,cudnn，然后正常安装tensorflow（忘了是pip还是conda装能跑通了）

最难受的是用pip安装tensorflow-gpu，然后再安装sionna时，pip会自动升级tensorflow版本，好像也会导致问题。

[conda安装cuda](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#using-conda-to-install-the-cuda-software)

[conda安装cudnn](https://docs.nvidia.com/deeplearning/cudnn/installation/latest/linux.html#conda-installation)

# docker安装tensorflow环境

> 先决条件：安装docker

> 先决条件：安装nvidia container toolkit
[按照官方文档安装](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)

## 安装tensorflow
[参考官方文档的docker安装](https://www.tensorflow.org/install/docker)

需要注意的是，tensorflow的版本和cuda的版本是有对应关系的，所以在安装时需要注意这一点，可以在官方的dockerhub上查看对应cuda最低版本的要求，你本地的nvidia-smi的cuda版本需要比tensorflow要求的cuda版本高，否则会报错

如[2.15.0版本的tensorflow的详情页](https://hub.docker.com/layers/tensorflow/tensorflow/2.15.0-gpu-jupyter/images/sha256-2de4ac3c6e8360a1e57b7dc4fca8d061daf7c58b61de31da1f0aca11c18bab32)，在第8条命令开始就有对应的cuda版本要求

ENV NVIDIA_REQUIRE_CUDA=cuda>=12.3

那么我本地cuda是12.2, 就不支持这个2.15版本的容器

因此我最后选择了2.14.0版本的容器，其他如目录挂载的命令等都是和正常跑docker是一样的

就是要加上--gpus all参数，这样才能让docker使用gpu

```bash
docker run --gpus all -it -d -p 8888:8888 -v /home/ma/Documents/opensora/10M_val_human:/home/ma/Documents/opensora/10M_val_human -v /home/ma/Documents/code/h264:/home/ma/Documents/code/h264 tensorflow/tensorflow:2.14.0-gpu-jupyter  bash
```

随后在终端内安装sionna，然后运行即可

```bash
pip install sionna
```

安装需要的其他库如Opencv-python

```bash
pip install opencv-python
```

有可能会有些lib库的依赖镜像中本来没有，因此需要apt安装对应的库

比如我就遇到了如下报错

```
Traceback (most recent call last):
  File "/home/ma/Documents/code/h264/SionnaPlus_sora.py", line 13, in <module>
    import cv2
  File "/usr/local/lib/python3.11/dist-packages/cv2/__init__.py", line 181, in <module>
    bootstrap()
  File "/usr/local/lib/python3.11/dist-packages/cv2/__init__.py", line 153, in bootstrap
    native_module = importlib.import_module("cv2")
                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/importlib/__init__.py", line 126, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ImportError: libGL.so.1: cannot open shared object file: No such file or directory
```

这个报错是因为opencv-python依赖于libGL.so.1，而这个库在镜像中没有，因此需要安装

```bash
apt-get update
apt-get install libgl1-mesa-glx
```

这种问题gpt直接可以解决

总的来说，docker安装tensorflow环境确实是最简单的，但是需要注意cuda版本的对应关系，以及可能会有一些库的依赖问题，但是这些问题都是可以解决的