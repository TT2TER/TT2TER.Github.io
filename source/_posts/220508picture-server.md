---
title: 我的博客图床
tags: blog
categories: 教程
excerpt: 图床解决方案
date: 2022-05-08 00:18:46
---

# 我目前博客图床解决方案
## PicGo + SM.MS
先说说[PicGo](https://picgo.github.io/PicGo-Doc/en/guide/#picgo-is-here), 一开始选它是因为它能和Typora结合，自动将本地图片上传并将Markdown文件中链接改为图床链接，可惜没用几天Typora收费了……

但奈何PicGo太好用，就自行研究了一下

形成了如下工作流程（一些快捷键自行在对应软件设置）
* **笔电截图快捷键/PrScr** Win自带的“截图和草图”功能，可以画批注，带自动复制图片到剪贴板功能
* 后台开启PicGo情况下 **Ctrl+Shift+P** 自动将剪贴板上图片上传到默认图床（可选，推荐SM.MS）并将图床链接以Markdown语法（可选默认语法，如HTML)复制到剪贴板
* 在所需要的位置 **Ctrl+V** 打法，插入图片

选用SM.MS 第一是因为它比较成熟；第二是因为国内外均可访问；第三是其他图床方案如七牛云需要自己配置服务器域名，且域名必须在国内备案，很麻烦

具体配置请参见PicGo官方文档

# 稳定性考虑准备换到对象储存
[参考链接](https://www.antmoe.com/posts/de414de5/)
TODO: