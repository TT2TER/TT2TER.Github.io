---
title: 再识proxy--tuic协议
tags:
  - vps
  - proxy
  - ipv6
  - tuic
categories: 教程
excerpt: tuic是一个基于quic协议的高性能代理
date: 2022-08-23 01:27:23
---

# tuic！tuic！
因为此前我尝试用香港的可怜的256mb内存的vps跑docker，导致香港的服务器崩溃，我一直放着没有管他。

今天有时间重启维护它，干脆重装一下系统。想到煎包之前又体验了个新的协议tuic，我便询问它和hyhi的优劣来，他说：
>延迟更低，而且支持0-RTT

我听的云里雾里，在他的建议下我便开始了我的尝试

# 声明

本文档为本人学习笔记，仅供学习使用，请勿用作违法用途。请任何看到本文档的组织或个人在30秒内立即停止使用本文档提及的技术做违反当地法律的内容，请勿将文档及相关链接发至百度贴吧等公开论坛。

# 相关链接
* [tuic的github仓库](https://github.com/EAimTY/tuic)
* [我参考的教程:内容已有些过时](https://lala.im/8424.html)

# 安装
## 服务端
>基本按照上面略有过时的教程来

1.下载
```bash
apt -y update
# 这个-y是用来免去输入y确认的参数
apt -y install wget certbot

mkdir /opt/tuic && cd /opt/tuic

wget https://github.com/EAimTY/tuic/releases/download/0.8.5/tuic-server-0.8.5-x86_64-linux-gnu
chmod +x tuic-server-0.8.5-x86_64-linux-gnu

# 注意这里下载的时候请下载对应（0.8.5）的最新版本，
# 见https://github.com/EAimTY/tuic/releases/ 注释：马火星
```

>第一遍我没有下载最新版本，下次看别的教程要注意，我也会在代码中提醒后人

2.新建config.json(服务端配置)
```bash
vim config.json
```
填入：
```json
{
    "port": 443,
    "token": ["example"],
    "certificate": "/opt/tuic/fullchain.pem",
    "private_key": "/opt/tuic/privkey.pem",
    "ip": "0.0.0.0",
    "congestion_controller": "bbr",
    "alpn": ["h3"]
}
```
若使用ipv6请将 `0.0.0.0` 改为 `::` (代表任意ipv6地址)[参考tuic文档](https://github.com/EAimTY/tuic#how-can-i-listen-both-ipv4-and-ipv6-on-tuic-server--tuic-clients-socks5-server)
![](https://s2.loli.net/2022/08/23/MK2vbhkqZdj4zEs.png)

>这个坑是煎包之前踩过的，但他开始没告诉我，信誓旦旦的说这里有个小坑，于是我踩进去了，在走了第一遍流程之后才知道

3.新建systemed配置
```bash
vim /lib/systemd/system/tuic.service
```
写入配置：
```
[Unit]
Description=Delicately-TUICed high-performance proxy built on top of the QUIC protocol
Documentation=https://github.com/EAimTY/tuic
After=network.target

[Service]
User=root
WorkingDirectory=/opt/tuic
ExecStart=/opt/tuic/tuic-server-0.8.5-x86_64-linux-gnu -c config.json
Restart=on-failure
RestartPreventExitStatus=1
RestartSec=5

[Install]
WantedBy=multi-user.target
```

>注意版本号

用get.acme.sh申请证书（也可以参考上面的教程）

详见我上一篇相关[博客](https://blog.1314171.xyz/post/220509freeipv6vps.html#4-%E4%BB%8E-letsencrypt-%E7%94%9F%E6%88%90%E5%85%8D%E8%B4%B9%E7%9A%84%E8%AF%81%E4%B9%A6)

转存证书记得按照如下路径转存fullchain和privkey

```bash
acme.sh --install-cert -d yourdomain.com
--fullchain-file    /opt/tuic/fullchain.pem    \
--key-file       /opt/tuic/privkey.pem  \
```
>在这里我遇到了跑通前的最后一个坑，分辨清楚fullchain是谁）

>同时在这里第一次申请证书的时候我还套了cdn，阴差阳错的给CDN主机申请了证书）

4.启动tuic服务并设置开机自启：
```bash
systemctl enable --now tuic.service
```

相关指令还有：`systemctl status tuic.service`能展示服务状态，`systemctl stop/start/restart tuic.service`等

## 客户端(win)

在[github release](https://github.com/EAimTY/tuic/releases)下载你系统对应的客户端

下载与服务端对应版本的
如：https://github.com/EAimTY/tuic/releases/download/0.8.5/tuic-client-0.8.5-x86_64-windows-gnu.exe

通过2rayN分流

之前提到的那篇略有过时的博客写的很清楚，[请拉到该博客末尾查看](https://lala.im/8424.html)

至此基本上遇到的坑都该提示的提示了

over


![测速展示（本地北京移动千兆下行百兆上行）](https://s2.loli.net/2022/08/23/xjb2ocJkZ7NwtQp.png)

# v2rayn更新支持tuic
[对应的issue](https://github.com/2dust/v2rayN/issues/2477)

使用方法见[官方更新日志](https://github.com/2dust/v2rayN/releases/tag/5.30)

但我没整成功）sad