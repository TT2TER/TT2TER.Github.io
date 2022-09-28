---
title: 图床服务器出错过程和解决
tags:
- vps
- network
- sync
categories: 
excerpt: 因为装探针无法连接到github导致的一系列问题
---
# 起因
安装探针，一开始想装到nas上，但nas环境，网络（家宽，端口屏蔽）docker服务不好访问，转而想装到服务器上

然后脚本运行curl时报错了

`Connecting to github.com (github.com)|140.82.121.3|:443... failed: Net`

我猜测是host的问题（但其实大概率不是）

我就头铁改host然后重启网络服务（命令：`/etc/init.d/network restart`)

直接导致了服务器ssh和服务都下线了

[可能原因](https://blog.csdn.net/qing_yc/article/details/55522164)

vnc也连不上，工单也没法及时回复，我想着晚上就把问题解决，于是重装了系统，幸好图床上没有太多的图片

最后重装之后发现一开始无法连接的问题居然解决了，想到也可能是warp网卡出错了……，如果早想到就不用重装了没准

另外就是这个服务器是最轻量的系统，里面啥都没有，因此重启服务不确定性很高

# 解决
## 首先重装图床
得益于自己写的博客，5分钟解决战斗
## 其次上传原来博客中用这个图床的图片
哎
## 最后，用微力同步备份