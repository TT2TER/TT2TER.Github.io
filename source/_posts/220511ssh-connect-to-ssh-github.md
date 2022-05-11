---
layout: publish
title: 通过SSH连接远程仓库
date: 2022-05-11 01:14:16
tags: git
categories: 
- [教程]
- [Problems]
excerpt: git ssh 设置代理（win）
---

# 报错：ssh: connect to host github.com port 22: Connection timed out
解决
according to:[this gist](https://gist.github.com/laispace/666dd7b27e9116faece6)


ssh访问

需要修改~/.ssh/config文件, 没有的话新建一个. 同样仅为github.com设置代理:(在linux or macos下)

```
Host github.com
    User git
    ProxyCommand nc -v -x 127.0.0.1:10808 %h %p
```
但是win没有nc命令，所以

如果是在Windows下, 则需要修改用户目录下.ssh\config, 其中内容类似于:

```
Host github.com
    User git
    ProxyCommand connect -S 127.0.0.1:10809 %h %p
```

这里-S表示使用socks5代理, 如果是http代理则为-H. connect工具git自带, 在\mingw64\bin\下面.

# SSH原理
[博客链接](https://blog.csdn.net/m0_50945504/article/details/119117874)
