---
title: 校园网通过IPV6代理实现免流且顺利浏览谷歌学术和GitHub
date: 2022-05-03 23:59:22
tags: 
- vps
- proxy
- ipv6
categories: 教程
excerpt: ipv6代理的方式校园网免流
---
# 校园网通过IPV6代理实现免流且顺利浏览谷歌学术和GitHub

# 声明

本文档为本人学习笔记，仅供学习使用，请勿用作违法用途。请任何看到本文档的组织或个人在30秒内立即停止使用本文档提及的技术做违反当地法律的内容，请勿将文档及相关链接发至百度贴吧等公开论坛。

# 一些有用信息来源

* [白嫖vps（每7天更新）](hax.co.id)
* [白嫖vps（每7天更新）同一家据说这个用的人少，浅浅尝试了一下确实速度完全可以接受](https://woiden.id/register?=iweec)
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
* [yyds提速工具HiHysteria](https://github.com/emptysuns/Hi_Hysteria)
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

只推荐香港,

原因1，近，线路先天的好，延迟先天的低；

原因2，在写这个文档的时候我买了个这家LA的机子，一套组合拳下来慢的要死（相较于香港，只能1080P油管

![这就是差距……上面是香港，下面是LA](https://s2.loli.net/2022/05/09/1amZlzRuM7AX3VT.png)

<HR style="border:3 double #987cb9" width="80%" color=#987cb9 SIZE=3>

5月9日更新：
其他地区也可以买了，有提速工具！有其他地区IP需求的可以考虑[点击跳转](#jump)

<HR style="border:3 double #987cb9" width="80%" color=#987cb9 SIZE=3>

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
## 1. 首先可以先测试下vps性能（可选），优先是否使用ipv6，以及更新软件源
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

## 2. 安装并运行x-ui
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

## 3. 使用warp为服务器添加IPV4（适用于Hax等无ipv4nat服务器，其他请跳过）

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

## 4. [从 letsencrypt 生成免费的证书](https://github.com/acmesh-official/acme.sh/wiki/%E8%AF%B4%E6%98%8E)

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


## 5. 设置入站流量

在x-ui面板中按图示设置

example.yourdomain.com改为你的域名，证书路径改为你的证书路径（如果你按照我的流程就不用改变)

备注随意

<img src="https://s2.loli.net/2022/05/03/IQJktDF31E8mjbs.png" alt="image-20220503171924473" style="zoom:150%;" />

设置好后点击查看，复制链接

在v2rayN中选择导入

![image-20220503172327717](https://s2.loli.net/2022/05/03/jCzZuOwPe1syr2b.png)

最终配置和下图以及你自己的配置一一对应即可

![image-20220503172232176](https://s2.loli.net/2022/05/03/gn8cIA91lNKVPua.png)

## 6. 如果速度不达预期，使用cf加速

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

## 7. enjoy！


# <span id="jump">如果还觉得慢：</span>！
# 再提速！
## 效果展示和前序准备
![未提速时](https://s2.loli.net/2022/05/09/kVHxNIfL53cTjz4.png)
![提速后！！](https://s2.loli.net/2022/05/09/afWlgkZLPmw3KCp.png)

*这个提速工具理论上会明显提高VPS流量消耗，因此除非上述步骤无法满足油管4K正常浏览，请不要使用这个工具*

在进行这步之前，请确保你完成了**部署过程**的步骤1和4，同时请确保在Cloudflare中的代理被关闭，如下图第一行示例（因此这个加速工具和上文提到的cf加速有一定的冲突

![](https://s2.loli.net/2022/05/09/C7q4dVLfptQnOKw.png)

[项目地址：HiHysteria](https://github.com/emptysuns/Hi_Hysteria)可以看到项目介绍

## 开始部署
### 0. 测试服务器状态

用本地的windows Powershell或其他终端 ping 你的服务器IPv6地址
```
ping x:x:x:x:x:x:x:x
```
往返行程的估计时间(以毫秒为单位):

    最短 = 174ms，最长 = 174ms，平均 = 174ms

记住此处的平均延迟

通过前文步骤1的性能测试或主机提供商信息预测自己服务器上行下行速度

了解自己本地带宽

### 1. 安装+设置

```
bash <(curl -fsSL https://git.io/hysteria.sh)
```
![](https://s2.loli.net/2022/05/09/EdHTuxveQq6ilcO.png)

此后几个选项按照如下示例填写

注意三个黄色的地方请按照自己实际情况填写

平均延迟就是步骤0中的平均延迟

客户端期望下行速度（一定要按照你的需求设置，原因见Github文档，我的建议速度如下）

   首先不能超过VPS的上行速度
   其次不能超过本地带宽，如千兆就是1000，百兆就是100等
   这是两条红线
   油管4k 150足以
   如果有高速下载需求
   300足以
   请根据自己需求设置，仅供参考！！！

客户端期望上行速度（也一定要按照你的需求设置，原因见Github文档，一般上行需求不大，没特殊要求设为下行的一半到3/4即可

![](https://s2.loli.net/2022/05/09/vq9IuFm6gBhGpZf.png)

### 2.使用
![](https://s2.loli.net/2022/05/09/g3ypfzic1UImKXx.png)
可以使用sftp将配置文件从/root下载到电脑本地

也可以复制粉色框内的内容粘贴到文本文档中

文档重命名为.json格式![](https://s2.loli.net/2022/05/09/5ms3vrTp7YQAiMw.png)

打开电脑本地的.json文件，修改这两个地方
![](https://s2.loli.net/2022/05/09/mESRJsU2kwNunbg.png)

#### 下面仅仅介绍用V2rayN连接方法
从[https://github.com/emptysuns/Hi_Hysteria/releases](https://github.com/emptysuns/Hi_Hysteria/releases)上下载这个

![](https://s2.loli.net/2022/05/09/yU3aACYuTzpb81x.png)

将里面的acl文件夹整个解压到你的V2rayN-Core安装目录下
![](https://s2.loli.net/2022/05/09/saqvG8dDWY6cye9.png)

从[https://github.com/HyNetwork/hysteria/releases](https://github.com/HyNetwork/hysteria/releases)上下载hysteria-tun-windows-6.0-amd64.exe，同样放在V2rayN-Core安装目录下（和acl一样）

添加自定义配置服务器
![](https://s2.loli.net/2022/05/09/AnLf3NymtZUoXWv.png)
地址选你刚刚下载到本地修改好端口的.json
![](https://s2.loli.net/2022/05/09/U98PK4wRZhxgXmo.png)

### 3.enjoy!!

## 因为这个脚本在开发阶段，bug较多，发生错误请自行解决，加油

# 一些其他问题

服务器重启，表现为连不上了，不一定是墙了，也可能是

服务器dns解析出问题

连接不上代理

[解决方法](https://www.laozuo.org/6647.html)

第一个方法就行