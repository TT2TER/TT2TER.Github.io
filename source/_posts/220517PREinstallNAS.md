---
title: nas安装前资料查询工作
tags: 
- nas
- TheWayToNAS
categories:
  - - 教程
  - - 学习过程
excerpt: 这里整理了nas到手前查询到的有用的文档和链接，和前置的思考
date: 2022-05-18 01:45:45
---

# 思考
[这是个教程整合](https://post.smzdm.com/p/av7or4dp/)
[这也是个整合](https://post.smzdm.com/p/ag8lzp8m/)

[这是个优化整合，其中pt,baiduyun备份，QNAP NAS 性能优化 ★★★（必看）](https://post.smzdm.com/p/aekwd90k/)
## 决定不组阵列
[参考了网友的讨论](https://www.zhihu.com/question/309305282)，加上自己对读写速度和容错没特别要求，尤其是但凡做了储存池或者Raid，基本意味着一个盘坏掉数据全无或修复成功率很低，加之占用空间，得不偿失

参考：
[NAS的硬盘损坏率真的有这么高吗？ - 林大路的回答 - 知乎](https://www.zhihu.com/question/309305282/answer/1480403268)

其中值得参考的：
>1. 标配一个UPS，几百元都行，山特、雷迪司、施耐德都行
>2. 不要做Raid，不要做Raid，做Raid大概率要坏坏一堆
>3. 做冷热数据分区或者用系统自带的冷热数据解决方案（SSD+HHD)
>4. 对于重要数据和普通数据分开保存，重要数据自动镜像到每个硬盘保留至少一份副本。重要的数据往往都不大，不会占用多大空间。
>5. 收集的电影除了多媒体文件最好还是保留种子文件，种子文件作为重要文件对待，如第4条。
>6. 建立一条计划任务，每月做一次S.M.A.R.T信息检查。
>7. 收到告警信息及时替换硬盘，反正故障硬盘质保内免费换新，不换白不换。

>走地鸡​:存储池实在危险。想起来就怕/郁郁葱葱回复走地鸡​:对的呀，数据分开来写入两块盘，坏一块盘，就全完了，比basic还要不靠谱

[关于ans的文件结构，软件到硬件](https://zhuanlan.zhihu.com/p/452053504)

## 整个流程
[威联通装机过程,主要关于备份和安全登陆](https://www.yinxiang.com/everhub/note/0aebb0ca-bcaa-4c68-9d4b-ba66f50242c1)
[超级长文！一站式NAS入坑指南，NAS选购、硬盘选购、常见玩法教程一网打尽！ - Karl说数的文章 - 知乎](https://zhuanlan.zhihu.com/p/424123077)

## 拿到二手初始化
如需连同先前创建的设置(包含用户、用户群组、共享文件夹等设置) 一并清除，按住RESET10秒即可(但磁盘数据将被保存)。

此处建议按10秒，将所有设置都清除，这样可以极大降低出问题的概率。

## 系统安装位置
在意系统位置的玩家，可以选择单盘启动（比如SSD）

## 权限管理
[总得分享](https://post.smzdm.com/p/ax0xemx3/)

## 看看外网访问的证书

## linux
[也许有需求](https://post.smzdm.com/p/ax0x7zgw/)


---
<li><a href="/post/TheWayToNAS">返回TheWayToNAS系列目录</li></a>