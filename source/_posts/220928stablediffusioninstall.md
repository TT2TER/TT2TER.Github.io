---
title: 最近大火的stable-diffusion（AI画图模型）安装
tags:
  - AI art
  - stable diffusion
  - deep learning
categories: 教程
excerpt: 因为英语写作要介绍个专业技术，最近这个AI画图技术飞速增长，就打算写它。为了更好了解，于是在本地跑了一下。本篇介绍win安装踩坑
date: 2022-09-28 01:49:51
---

# 前排提示，因为图床暂未配置证书，故请暂时关闭https保护以加载本文http图片资源（部分浏览器无法关闭）
如火狐可以在左上角小锁选项中选择暂时解除保护
![](http://euserver.1314171.xyz/i/2022/09/28/633337411418d.png)

# 选择的web-ui
选择了一个看起来优化不错的ui

[stable-diffusion-ui](https://github.com/cmdr2/stable-diffusion-ui)

# win安装过程
## 请先阅读官方说明
[说明](https://github.com/cmdr2/stable-diffusion-ui#installation)
## 过程
> 说明，本方法为 为所有涉及终端配置代理，不喜勿看
1. 到[releases](https://github.com/cmdr2/stable-diffusion-ui/releases)找到win系统对应链接下载

[下载链接,v2.16版本（不建议点击这个下载）](https://github.com/cmdr2/stable-diffusion-ui/releases/download/v2.16/stable-diffusion-ui-win64.zip)

2. 解压到硬盘根目录，即`c:`or`d:`，e.g.`C:\stable-diffusion-ui`,避免触及win系统路径长度限制
3. 如果肉身在国外或有透明代理，双击`Start Stable Diffusion UI.cmd`即可，其余网络环境请继续阅读
4. 如果系统中未安装`1. git客户端 2.anaconda（Python虚拟环境）`请先行安装，方便代理配置
5. 为如下客户端配置代理 
    1. git http 
    2. git ssh
    3. anaconda
    4. cmd

方法：

i. git http代理（永久）
```git
#开启
git config --global http.proxy "socks5://127.0.0.1:yourport"
git config --global https.proxy "socks5://127.0.0.1:yourport"
git config -l --globle #查看是否配置成功
#如需要关闭：
git config --global --unset http.proxy
git config --global --unset https.proxy
```
ii. git ssh代理（永久）

[参考本人博客：为git ssh设置代理](https://blog.1314171.xyz/post/220511ssh-connect-to-ssh-github.html)

iii. anaconda代理（永久）

打开图形界面（navigator)
![](http://euserver.1314171.xyz/i/2022/09/28/633332fc05410.png)

点击prefer……
![](http://euserver.1314171.xyz/i/2022/09/28/6333335e6cd0a.png)

选择下方绿色选项：`config conda`

粘贴下方配置
```
channels:
  - conda-forge
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
ssl_verify: false
proxy_servers:
    http: http://127.0.0.1:yourport
    https: http://127.0.0.1:yourport
```
注意替换你的端口，各个配置项含义请自行百度

iv. cmd代理（仅限该终端）
如果你用的clash，可以点击这个terminal图标
![](http://euserver.1314171.xyz/i/2022/09/28/6333343deb9c8.png)
直接选择打开配置好代理的cmd终端

或者新建终端键入
```bash
set http_proxy=http://127.0.0.1:yourport & set https_proxy=http://127.0.0.1:yourport
```

6. 在步骤`5.`配置好代理的终端中将路径切换到stable diffusion根目录

如
```bash
e:#你的，如d:
cd stable-diffusion-ui
```
如图
![](http://euserver.1314171.xyz/i/2022/09/28/6333357693588.png)

7. 键入完整目录，注意用引号括住
```bash
"E:\stable-diffusion-ui\Start Stable Diffusion UI.cmd"
```
（也可以拖动.cmd）到命令行中
回车

等待安装即可
## 其他说明
1. 如果安装报错失败，请完全删除`stable-diffusion-ui`文件夹及其内容，重新从步骤`2.`解压开始安装
2. 安装后再次运行`.cmd`文件即可再次使用，注意每次运行都会自动检查更新，因此每次运行时需要按照上述步骤`6.`开始配置cmd代理，以保证各项模块正常检查更新。
3. 如不需要更新，可以关闭系统代理core(即完全退出代理软件)，直接双击`.cmd`也可运行