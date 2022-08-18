---
title: 自建rss服务器(freshrss+rsshub)
tags:
  - nas
  - docker
excerpt: 最大化利用自己的nas，正好现在用的inoreader国内被墙了
date: 2022-08-11 00:46:39
categories:
---

# 为什么选freshrss
一开始打算使用TTRSS,但ttrss上手太麻烦，还要设置登陆的URL必须对应，而我既要公网访问又要内网来设置它，也不想研究这些具体是啥。其实TTRSS官方的文档应该写的挺清楚的，真正让我转移目标的原因是docker跑不起来，解决了一步log又爆出新的错根本跑不动。其中有一个是说Docker自己建的文件没有写入权限。这个之后再讲。还有就是奇奇怪怪的和数据库不搭配之类的。可是我用的官方的DockerCompose,还出问题，并且因为URL的事情我并不能看到图形界面来调试，最终放弃。

**TTRSS 的报错**
```
Please fix errors indicated by the following messages:

    ICONS_DIR defined in config.php is not writable (chmod -R 777 feed-icons).

You might want to check tt-rss wiki or the forums for more information.

Please search the forums before creating new topic for your question.
```

后来再百度关键词"docker rss"又有了freshrss这样的新选择，尝试之后发现我至少能看到图形界面了

而在图形界面部署中间又遇到了没有写入权限的问题。我依旧赋予777权限等办法轮番尝试，依旧不行。最后我反思整个过程：
1. 我之前部署的镜像也有挂载路径的需求，而且也需要写入文件，原来就没报错过。所以应该不是我操作上的问题。
2. 已知的谷歌到的赋权方法我都试过了，没有效果。
3. ls -al检查发现文件的所属用户组是奇怪的数字，我本机没有这样编号的用户组。

回想之前我在整相册的时候该过系统文件夹权限的设置，我意识到可能是这里出问题了
<li><a href="/post/220807photosync"  tags="里面的教程叫我：“请首先开启高级文件夹权限，才可以单独设置每个文件夹权限”"></li>“请首先开启高级文件夹权限，才可以单独设置每个文件夹权限”

关闭这个选项后，万事大吉

freshrss解决权限问题就能用了，而重新试了试TTRSS发现，解决权限问题还跑不起来，累了

于是就用freshrss了

# 安装
[freshrss部署教程](https://cloud.tencent.com/developer/article/1964176)

官方的部署写的不是很清楚，按这个来亲测能用，自己改一下挂载路径和端口即可
```
version: "3"

services:
  freshrss-db:
    image: postgres:latest
    container_name: freshrss-db
    hostname: freshrss-db
    restart: always
    volumes:
      - /share/Docker/rss/postgresql/data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: freshrss
      POSTGRES_PASSWORD: freshrss
      POSTGRES_DB: freshrss

  freshrss-app:
    image: freshrss/freshrss:latest
    container_name: freshrss-app
    hostname: freshrss-app
    restart: always
    ports:
      - 18110:80
    depends_on:
      - freshrss-db
    volumes:
      - /share/Docker/rss/data:/var/www/FreshRSS/data
      - /share/Docker/rss/extensions:/var/www/FreshRSS/extensions
    environment:
      CRON_MIN: '*/20' #自动更新时间
      TZ: Asia/Shanghai
```

# 使用

使用时发现有些源需要代理，于是有了整代理的理由。

代理因为内存占用过多且我浅试了一下连不上，决定在vps上重新部署rss服务器了

然后突然想起来我vps是纯v6的，还得设置端口转发

再一看256mb内存很吃紧了，遂放弃

## fever API接口：
TODO: