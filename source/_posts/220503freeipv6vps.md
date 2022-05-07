---
title: 校园网通过IPV6代理实现免流且顺利浏览谷歌学术和GitHub
date: 2022-05-03 23:59:22
tags: vps
categories: 教程
excerpt: ipv6代理的方式校园网免流
---
# 校园网通过IPV6代理实现免流且顺利浏览谷歌学术和GitHub

# 声明

本文档为本人学习笔记，仅供学习使用，请勿用作违法用途。请任何看到本文档的组织或个人在30秒内立即停止使用本文档提及的技术做违反当地法律的内容，请勿将文档及相关链接发至百度贴吧等公开论坛。

# 一些有用信息来源

* [白嫖vps（每7天更新）](hax.co.id)
* [便宜低性能高带宽vps(native ipv6+NAT ipv4)](https://webhorizon.in/)
* [白嫖子域名（不推荐）](https://freedns.afraid.org/)
* [白嫖顶级域名](https://www.freenom.com/zh/index.html?lang=zh)
* [白嫖/便宜域名](https://nic.ua/)
* [假身份生成器](https://fake-it.ws/)
* [x-ui面板](https://github.com/vaxilu/x-ui)
* [warp连接CF WARP为服务器添加IPv4/IPv6网络](https://github.com/fscarmen/warp)
* [从 letsencrypt 生成免费的证书](https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E)
* [vps简单性能测试脚本bench.sh](https://teddysun.com/444.html)    [github页面](https://github.com/teddysun/across)
* [CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest)
* 本文档特别感谢煎包的支持
  



# 在开始前，你应该：

## 0.有基本的计算机及互联网知识

如通过ssh连接主机，懂得管理DNS记录等

## 1.拥有自己的顶级域名

* [白嫖子域名（不推荐）](https://freedns.afraid.org/)
* [白嫖顶级域名(推荐)](https://www.freenom.com/zh/index.html?lang=zh)
* [白嫖/便宜域名](https://nic.ua/)

任选一个注册，可以用假身份，但邮箱要自己的
* [假身份生成器](https://fake-it.ws/)

然后将域添加到[cloudflare](https://www.cloudflare.com/zh-cn/)
## 2.拥有一台合适的vps
### a.免费练手VPS
[白嫖vps（每7天更新）](hax.co.id)

需要电报账号注册，推荐先来练手

### b.推荐大带宽低性能小硬盘VPS
[便宜低性能高带宽vps(native ipv6+NAT ipv4)](https://webhorizon.in/)

推荐购买香港的NAT服务器7刀每年，支付需要银联卡（PayPal）
只推荐香港

服务商是印度阿三，会有一些小毛病如据说会每月定期重启一次你的vps，emmm，价格实惠 ，要啥自行车

保姆级步骤，放心食用

1. 选购

![image-20220503145942061](https://s2.loli.net/2022/05/03/bYhS9kQsOwRUKi1.png)

![image-20220503150456728](https://s2.loli.net/2022/05/03/CvfRtMhdX4wLkne.png)

![image-20220503150607806](https://s2.loli.net/2022/05/03/CrDq8kiHW6wajPE.png)

![](https://s2.loli.net/2022/05/03/zSMqw7sZvdCQnT8.png)

![image-20220503150739980](https://s2.loli.net/2022/05/03/672N5kPCm4UZJQv.png)

我因为已经有一个香港的了，所以我下面用一个洛杉矶的作为演示

example.com处写你自己的域名

最好用debian系统

![example.com处写你的域名](https://s2.loli.net/2022/05/03/vLVOe4aurmE8yqX.png)

注册账号，可以用假信息，但邮箱要真的

![image-20220503151928736](https://s2.loli.net/2022/05/03/wkYRTsjEguS5qWU.png)

![image-20220503152130156](https://s2.loli.net/2022/05/03/QM3ylSfFCvKOYsm.png)

2. 支付

![image-20220503152228730](https://s2.loli.net/2022/05/03/kGISHr2COBQ7hDK.png)

![image-20220503152425381](https://s2.loli.net/2022/05/03/4JozxZCD96IhjrK.png)

![image-20220503153033537](https://s2.loli.net/2022/05/03/WAKadR3glmxPHth.png)

填写短信验证码后再次填写一遍相关信息，点击使用CNY付款

再次填写验证码（我也不知道为啥有两个，但实际上就是只支付了一遍，放心）

后面注册PayPal否，自行选择

返回商家

![image-20220503153744704](https://s2.loli.net/2022/05/03/th7f2mQbcWeXJGz.png)

在order history 中可以看到订单状态为 In Review 耐心等待，阿三的工作效率比较低，可以三四小时后再查看是否开机

开机之后用ssh连接

使用过程中有问题及时提ticket！

# 部署过程
1. 首先可以先测试下vps性能（可选），优先是否使用ipv6，以及更新软件源
```
apt update
apt upgrade

#源码和用法见文章开头：vps简单性能测试脚本bench.sh
wget -qO- bench.sh | bash

#ip检测
#若无curl 运行 
apt install curl
curl ip.gs
#若返回ipv6地址则优先ipv6
#若非ipv6优先如何设置？TODO:
curl -4 ip.gs
#如返回：curl: (7) Couldn't connect to server则没有ipv4
ping www.youtube.com
ping ipv6.baidu.com
#测试国内外链接情况
```

2. 安装并运行x-ui
   [x-ui面板](https://github.com/vaxilu/x-ui)
```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
#他会显示以下内容：
#出于安全考虑，安装/更新完成后需要强制修改端口与账户密码
#确认是否继续?[y/n]:
#(回车默认n，最好y更改一下
#设置开机自启动,应对阿三每月重启（无论如何自启动都是必要的）
x-ui enable
```

步骤如图![image-20220503155155000](https://s2.loli.net/2022/05/03/J1NPWku7Vs5h8fO.png)

在浏览器中输入[2a01:4f8:242:4986:face:face:13cf:1]:14567（换成你的主机地址和设置的端口号）并输入账户名密码进入面板

![image-20220503155522948](https://s2.loli.net/2022/05/03/V5IlZRgJNAH1qpi.png)

3. 使用warp为服务器添加IPV4（适用于Hax等无ipv4nat服务器，其他请跳过）

[warp连接CF WARP为服务器添加IPv4/IPv6网络](https://github.com/fscarmen/warp)

```
wget -N https://raw.githubusercontent.com/fscarmen/warp/main/menu.sh && bash menu.sh 6
```

选择安装参数

![image-20220503161046719](https://s2.loli.net/2022/05/03/eDAcNvQ5L3Xj6dn.png)

安装结果

![image-20220503161903878](https://s2.loli.net/2022/05/03/8XT6uabgYrKULPJ.png)

可以

```
ping 8.8.8.8
```

做测试，通了就成了

4. [从 letsencrypt 生成免费的证书](https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E)

```
apt install socat
//具体使用方法看官方文档
curl  https://get.acme.sh | sh -s email= my@example.com
#替换为你的邮箱
~/.acme.sh/
alias acme.sh=~/.acme.sh/acme.sh
```

在运行下一个命令之前，使用cloudflare解析一个子域名到你的服务器，使用AAAA解析
如example.yourdomain.com

```
acme.sh  --issue -d example.yourdomain.com  --standalone --listen-v6
#换成你的子域名
```

成功演示（因为这是演示，一会就删，所以就不打码了）

![image-20220503164523932](https://s2.loli.net/2022/05/03/jpxaTkK68nItqA3.png)

可以选择把证书拷到别的地方,如根目录

```
acme.sh --install-cert -d example.yourdomain.com \
--cert-file      /root/cert.pem  \
--key-file       /root/key.pem  \
#域名改为你的域名
```

![image-20220503171353387](https://s2.loli.net/2022/05/03/5QCdvW6UVhZ1Bon.png)

cert是公钥路径，key是密钥路径

5. 设置入站流量

在x-ui面板中按图示设置

example.yourdomain.com改为你的域名，证书路径改为你的证书路径（如果你按照我的流程就不用改变)

备注随意

<img src="https://s2.loli.net/2022/05/03/IQJktDF31E8mjbs.png" alt="image-20220503171924473" style="zoom:150%;" />

设置好后点击查看，复制链接

在v2rayN中选择导入

![image-20220503172327717](https://s2.loli.net/2022/05/03/jCzZuOwPe1syr2b.png)

最终配置和下图以及你自己的配置一一对应即可

![image-20220503172232176](https://s2.loli.net/2022/05/03/gn8cIA91lNKVPua.png)

6. 如果速度不达预期，使用cf加速

在cloudflare上设置该选项为完全

![image-20220503172552145](https://s2.loli.net/2022/05/03/wvftEr93KD5gpUu.png)

域名解析设置cloudflare代理

![image-20220503172935479](https://s2.loli.net/2022/05/03/CPrVZYpDyJBEOUn.png)

x-ui新建：

![image-20220503175311903](https://s2.loli.net/2022/05/03/I2UcPJNVqXvrlC6.png)

![image-20220503175504819](https://s2.loli.net/2022/05/03/DG5AM8chNnqUxXF.png)

其中蓝圈部分是Cloudflare CDN的IP，可以选择自己最好用的，用我上图的也行，不过最好在自己本地测试一下

[CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest)

使用这个测试，记得加-ipv6参数（在你的电脑上运行哦，不是vps）

筛选得到最快ip填上去

发现快了好多

7. enjoy！



# 其他问题

服务器重启，表现为连不上了，不一定是墙了，也可能是

<img src="https://s2.loli.net/2022/05/03/fOQ78VqeBXK9E5g.png" alt="image-20220326212448712" style="zoom:50%;" />

导致服务器dns解析出问题

连接不上代理

[用这个解决](https://www.laozuo.org/6647.html)

第一个方法就行