---
title: 尝试新的图床解决方案
tags: blog
categories: 教程
excerpt: sm.ms经常寄，尝试github+jsdelivr
date: 2022-09-04 00:06:11
---

# 前言
我之前的图床解决方案

<li><a href="/post/220508picture-server"  tags="">我的博客图床</li>


# 过程
## 首先跟着这个博客来
其中有四点要注意

1. 可以不用勾选readme
2. token 还要选上user(我也不知道为啥而且我也没测不选能不能用，另一个教程选了，我怕麻烦也选了)
3. token设置在github的settings -> developer settings里
4. 特别注意cdn.jsdelivr.net国内被dns污染了，所以要把它换成fastly.jsdelivr.net

[教程](https://zhuanlan.zhihu.com/p/489236769)

## 其次，picgoyyds
本来想试试换用sharex截图上传，但网上[没有成型的用github图床的解决办法](https://nokiasonic.github.io/2021/09/24/%E3%80%90%E5%BA%94%E7%94%A8%E8%BD%AF%E4%BB%B6%E3%80%91ShareX%E6%88%AA%E5%9B%BE%E5%B7%A5%E5%85%B7%E7%9A%84%E4%BD%BF%E7%94%A8/)


于是，拥抱PicGo，bingo！

# 效果测试：

![](https://fastly.jsdelivr.net/gh/TT2TER/image1st@main/img/20220904000123.png)

图片内容为`# 效果测试：`几个字