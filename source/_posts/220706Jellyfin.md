---
title: 威联通nasJellyfin硬件转码+硬链接后刮削
tags: nas
categories: 教程
excerpt: 影视系统
date: 2022-07-15 00:24:32
---

# 教程
[对应版本,打包驱动版](https://post.smzdm.com/p/a3gw6g47/)

[安装教程](https://post.smzdm.com/p/apv8gg72/)

[配置介绍](https://post.smzdm.com/p/a859320l/)
## 解码器赋权
```
sudo chmod 777 /dev/dri/renderD128
```
## 安装
```
docker run --name jellyfin -d \
 --volume /share/Docker/Jellyfin/config:/config \
 --volume /share/Docker/Jellyfin/cache:/cache \
 --volume /share:/video \
 --net=host \
 --restart=always \
 --device /dev/dri/renderD128:/dev/dri/renderD128 \
 nyanmisaka/jellyfin
```

哎这个镜像是真的大啊，下载的好慢啊！

## 按照上面链接教程设置解码即可！

# 刮削 
首先建议先设置硬链接，方便同时做种刮削
<li><a href="/post/220714hlink"  tags="">硬链接教程</li>

# 同步观看SYNCplay
这个功能能够让两人同步观影。注意不能通过反向代理连接服务器，只可公网直连或者局域网连接。

使用方法，播放视频时右上角三个人头的图标，创建或加入，可以自行调同步方式和参数，建议最小延迟不要太小，否则会不时卡顿。

# 电视端TODO:https://post.smzdm.com/p/a99vlpmp/

# 附录
看到了一个大佬的[自动化流程](https://leishi.io/blog/posts/2021-12/home-nas-media-center/#%E5%9F%BA%E6%9C%AC%E6%B5%81%E7%A8%8B%E7%AE%80%E4%BB%8B)