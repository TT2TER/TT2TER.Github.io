---
title: 书接上文-nas系统崩溃重装
tags: nas
categories: Problems
excerpt: nas的系统在安装了一个包管理器后就出毛病了，记录修复的过程
date: 2022-07-03 12:11:42
---

# 其实是联系威联通客服啦，毕竟官方应该更熟悉机器，懒
官方的解决办法就是，先尝试重连，不行。

再ssh链接之后备份硬盘，然后重装系统

里面下的电影我不想删，就留着了，但之后做种不知道好不好整。

重装完了顺便整个tr吧

# 重装系统后流水账记录
1. 新建储存卷
2. 挂载旧的备份盘，并将文件设置为威联通共享文件夹路径

![](https://s2.loli.net/2022/07/05/L8cCab5x29fnuBD.png)
![](https://s2.loli.net/2022/07/05/im7nAjJfHXhCt5O.png)
3. 安装有必要的软件，如verysync,qbit并再次配置好
4. docker：portainer;iyuu;tr;ddns-go
5. 计划把种子一个一个手动导进来

---
<li><a href="/post/TheWayToNAS">返回TheWayToNAS系列目录</li></a>