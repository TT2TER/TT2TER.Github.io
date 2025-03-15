---
title: 配置更符合现代科研环境的NTSCC
tags:
  - ntscc
categories:
  - 教程
excerpt: NTSCC官方的环境好像有些问题，我这里记录一下解决方法。
date: 2025-03-15 16:00:36
---

# 配置ntscc
ntscc是一个图像的信源信道联合编码工具[https://semcomm.github.io/ntscc/](https://semcomm.github.io/ntscc/)

他官方的环境需要的torch版本和cuda版本都比较老了，有点脱离现在的科研环境

将官方的都升级了一下python3.8->3.10 torch1.71->2.2.2 cuda11.0->11.8

以下是经过我测试的配置方案。测试环境是"Ubuntu 22.04.5 LTS" RTX 4090 Driver Version: 535.183.01 CUDA Version: 12.2

本机只装了nvidia的显卡驱动，无cuda等其他工具

> 前置条件，安装conda
```bash
conda create -n $YOUR_PY38_ENV_NAME python=3.10
conda activate $YOUR_PY38_ENV_NAME

pip install torch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 --index-url https://download.pytorch.org/whl/cu118

python -m pip install -r requirements.txt
```

其中，requirements.txt对应内容需要修改为
```txt
# This file may be used to create an environment using:
# $ conda create --name <env> --file <this file>
# platform: linux-64
compressai==1.2.6
timm==0.9.16
numpy==1.24.3
```
特别将numpy版本降低到1.24.3（我也忘了是要适配哪个库需要降级了）

最后，因为用了更高版本的compressai，需要修改一下ntscc中import
```python
# 将文件net/NTSCC_Hyperior.py中
# from compressai.ops import ste_round
# 改成:
from compressai.ops import quantize_ste
# 同时也要修改一下调用的地方
# ste_round -> quantize_ste
```
