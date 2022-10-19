---
title: 初次安装nas系统
tags:
  - nas
  - docker
categories:
  - - 教程
  - - 学习过程
excerpt: nas初始化安装过程记录
date: 2022-07-04 20:51:10
---

# 过程简述
## 电源
插到了ups上，dp充电头有些松动
## 局域网连接初始化硬盘
两个8t简单卷，初始化慢慢的
## 第一个问题：学校局域网有网页登陆认证，系统没有浏览器无法访问外网
当时想到的解决方案有：
1. 用ssh登陆设置脚本认证
2. 用pc共享网络
3. 找个无线网卡连接无线网

最后先用了方法2，先把机器装好再说，之后打算用方案1

## 安装软件更新，配置hdim输出界面，更新系统（linux底层安全漏洞修复）
更新完系统重启的时候很慢，得有10分钟，不知道是因为更新还是每次重启都会这么慢。

配置hdmi界面后，有了奇奇怪怪的需求。我控制nas的输入设备是之前的旧的蓝牙键盘，我突然想到之前买键盘的时候如果买的是多模的，就可以无缝切换电脑和nas了。

## 配置好了微力同步，同步速率很快

## 安装了浏览器，能够在局域网内手动登陆校园网

## 用nas的虚拟交换机让电脑也能继续用有线

## 发现学校没有公网ipv6??

## qb套件下载
发现连不上tracker,放弃

换用Docker
## Docker折腾


换的时候ssh连接密码不对，三秒重置

然后之前的虚拟交换机寄了，好多功能自动关闭了

数据应该没问题

emm重新登陆发现初始密码就是之前输的，难道是输错了？

[找了一个人的教程，安装docker，他说自带的不好用（不够折腾）](https://post.smzdm.com/p/az3k85gr/)

这个人博客的命令运行不了

评论区的中文版能用

[后续Docker管理界面教程做的比较好](https://post.smzdm.com/p/a6dw97xo/)

但是qb docker根本不能用好吧，要不就是连不上tracker,要不就是webui上不去，而且现有办法都不行

最后尝试transmission根本打不开，乐

然后用威联通自带的下载中心，能连，说明网络不是问题（但不支持仅ipv6)

最后下了个很旧的套件版本，凑活能用，大部分站点都能连上tracker，有的要将https改为http，另外有的根本没法连（纯ipv6下）

后来更新到4.3.9又可以了

### 关于qb的下载问题
之前因为峰值速度和连接性的问题，qb总是卡死，有时候系统卡死，在配置了最大连接数等东西之后解决了这个问题。

配置重点是最大连接数和全局上传窗口上限符合系统承受能力，我的分别是800 500

每个的不限制

上传窗口策略是固定窗口数


## smb挂载

很简单，本地浏览速度可以

## smtp消息提醒

## 一些有意思的docker
音乐服务器……
DDns

*portainer*

docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /share/Docker/portainer_data:/data 6053537/portainer-ce
[汉化版](https://hub.docker.com/r/6053537/portainer-ce)

***2208207更新***
把汉化版替掉了，因为汉化不一直更新

更新过程参考官方文档：[Upgrading on Docker Standalone](https://docs.portainer.io/start/upgrade/docker)(官方版更新也是这个流程)

注意将存储路径改对

```bash
docker run -d -p 8000:8000 -p 9443:9443 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /share/Docker/portainer_data:/data portainer/portainer-ce:latest
```

*ddns-go*
```bash
docker run -d --name ddns-go --restart=always --net=host -v /share/Docker/ddns-go:/root jeessy/ddns-go
```

## 关于docker的更新
只需要在portainer container details中recreate的同时选择拉取最新镜像即可

![最新镜像拉取打开](https://pic.1314171.xyz/i/2022/10/19/634fe19df1b4f.png)

注意请保证配置文件等数据不在镜像内部内存中，否则会覆盖掉配置