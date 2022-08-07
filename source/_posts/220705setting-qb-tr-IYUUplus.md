---
title: qb&tr&IYUUplus结合
tags:
  - nas
  - pt
categories: 教程
excerpt: 在nas坏掉之后借机解决下载&转种的问题
date: 2022-07-09 14:21:01
---

# 主要是参考一下博客
[PT工具之Docker全家桶+HTTPS详细配置教程](https://blog.csdn.net/shangyexin/article/details/121924875)

[【原理篇】qBittorrent下载+转种Transmission快校版+IYUU Plus辅种教程](https://blog.csdn.net/shangyexin/article/details/122043327)

[【操作篇】qBittorrent下载+转种Transmission快校版+IYUU Plus辅种教程](https://blog.csdn.net/shangyexin/article/details/122085552?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-122085552-blog-122043327.pc_relevant_multi_platform_whitelistv2&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-122085552-blog-122043327.pc_relevant_multi_platform_whitelistv2&utm_relevant_index=1)

# 我的一些心得
* 用portainer新建很傻瓜
* 注意在iyuu里地址可以写127.0.0.1，毕竟在本地
* tr的docker对权限要求比较高，建议环境变量的puid/pgid都设成0.即admin

---
<li><a href="/post/TheWayToNAS">返回TheWayToNAS系列目录</li></a>