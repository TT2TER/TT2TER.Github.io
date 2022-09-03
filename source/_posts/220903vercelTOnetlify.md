---
title: 放弃刚用两天就被墙掉的vercel
tags:
  - blog
  - vercel
  - netlify
categories: 教程
excerpt: 用vercel没几天后dns就被污染了，换！
date: 2022-09-03 22:51:45
---

# 找了新的服务商：
[netlify](https://app.netlify.com)

看起来这个是以team为基本组织架构的服务商

免费方案可以部署好几个网站，轻度使用够了，大不了再注册个号。

他免费有些限制，比方不能并发（同时）构建网页（不影响同时托管），构建总时长有限制（意思是不能运行很复杂的，运行很多次，300Min限制）同时网页访问数据在100G每月，正常博客wiki等完全没问题。

# 注意的细节

本来想插图片的但，sm.ms好像多少出了点问题，TODO:速速备份。

描述一下，注意网页的根目录和build command

# 把原来的域名改绑定

原来vercel绑定的改为`yournamebackup`

域名同样有https,但比vercel慢点，等等就行了

直接在域名解析CNAME到你的`yourproject.netlify.app`就行