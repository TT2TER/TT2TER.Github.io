---
title: whisper实时转录
tags: openAI
categories: 教程
excerpt: 很好用的语音识别，英文准确率很高，可以用来识别英语听力
date: 2022-10-18 20:31:16
---

# introduce
这是一个本地的语音识别模型
强无敌

官网介绍：[Introducing Whisper](https://openai.com/blog/whisper/)

# openAI官方的python版本安装
github仓库链接:[whisper](https://github.com/openai/whisper)

1. 使用anaconda
2. 在anaconda环境中安装cuda(请耐心等待解压)
```
# 安装CUDA
conda install cudatoolkit=11.6 # 指定版本
```
3. pytorch
请到它的[官网](https://pytorch.org/get-started/locally/)选择下载对应的你的cuda的版本
4. 安装ffmpeg
```
conda install ffmpeg
```
5. 运行安装其他依赖库
```
pip install git+https://github.com/openai/whisper.git 
```
6. enjoy it！(模型会在运行时下载)
具体使用方法见github，下面是一个示例
```
whisper "3.3 Task 19 Gauss.mp3" --model base
```
# cpp实现
TODO:
