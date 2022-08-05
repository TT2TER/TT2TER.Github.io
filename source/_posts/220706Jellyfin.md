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

## TMM刮削器安装&使用
### 链接
[司博图视频教程](https://www.bilibili.com/video/av73683523?msource=smzdm_937_0_184__d08e65aac0e9e73f&vd_source=81d250ace1f03d943723e87ae82d6bfe)
教程有些古老了，不过也能用

以下链接经过筛选排名不分先后互补
[官网镇楼](https://www.tinymediamanager.org/)
[一个比较详细的配置教程](http://www.360doc.com/content/22/0403/01/75728668_1024595485.shtml)
[刮削配置到jellfinKodi一条龙](https://post.smzdm.com/p/a4wkqw37/?invite_code=zdm3d7ehjjinv)
[同样比较详细，同时附上了一些常见的Bug解决](https://post.smzdm.com/p/a7dr8qml/)
## 准备先尝试在电脑上安装
原因：在nas上安装没有很好的前人铺路，[其实有，是个很古早的教程，还比较麻烦,flag一下以防有需要](https://zhongce.sina.com.cn/article/view/39694)

## 文件访问权限不够
映射到电脑上之后没有访问权限，更改一下登陆用户到admin
[更改网络驱动器保存的账户密码](https://www.zhihu.com/question/315835685)



# 同步观看SYNCplay
这个功能能够让两人同步观影。注意不能通过反向代理连接服务器，只可公网直连或者局域网连接。

使用方法，播放视频时右上角三个人头的图标，创建或加入，可以自行调同步方式和参数，建议最小延迟不要太小，否则会不时卡顿。

# 电视端TODO:https://post.smzdm.com/p/a99vlpmp/

# 附录
看到了一个大佬的[自动化流程](https://leishi.io/blog/posts/2021-12/home-nas-media-center/#%E5%9F%BA%E6%9C%AC%E6%B5%81%E7%A8%8B%E7%AE%80%E4%BB%8B)