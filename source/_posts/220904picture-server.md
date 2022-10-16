---
title: 用仅ipv6vps自建图床并支持ipv4访问
tags:
  - vps
  - blog
  - vscode
categories: 教程
excerpt: 之前图床都不好用了，为了可持续发展，决定自建图床
date: 2022-09-05 23:33:30
---
# 前排提示，因为图床暂未配置证书，故请暂时关闭https保护以加载http图片资源

加密在整了TODO:

# 换图床的原因
之前sm.ms图床已经不太能用而且有审核，已经无故挂了我三张图片了

后来github图床的解决方案因为jsdelivr的cdn加速在国内被墙：

[致敬-被滥用的jsdelivr,我又何尝不是其中一员呢？](https://luotianyi.vc/6295.html)

干脆直接换个较大硬盘的vps

简单搜索之后发现方案可行，基本上随便一搜就20欧10G千兆带宽

# 选择主机商
舍友推荐了个便宜的主机商：

[server-factory](https://my.server-factory.com/)

仅ipv6主机仅需6欧，nat主机9欧一年，而且支持Alipay（支付宝）
![测速图片](https://euserver.1314171.xyz/i/2022/09/08/6319f8f453f3b.jpg)

要什么自行车，冲他
![购买这个就行](https://euserver.1314171.xyz/i/2022/09/08/6319f8d4f01d0.jpg)

买这个仅Ipv6就行，解决ipv4访问用cf cdn套一层代理

确保用c代理，小云朵打开即可

## 申请证书
之前用脚本在vps上申请证书的时候不能套上述小云朵，否则会失败或者替cf申请证书……

这次尝试直接套小云朵嫖cf证书

### 221001更新
![](http://euserver.1314171.xyz/i/2022/10/01/63384fdfbdd4d.png)
![](https://euserver.1314171.xyz/i/2022/10/01/6338539cb8b2f.png)
https://65536.io/2020/03/607.html

# 选择图床
大概有三个很好的选择，[兰空图床](https://www.lsky.pro/)、[imgurl](https://github.com/helloxz/imgurl)和[chevereto](https://chevereto.com/)

最后选择兰空的原因是：imgurl社区开源版本上次更新已经过去三年了，[chevereto](https://github.com/chevereto/vps)令人望而生畏的英文文档，以及，我以为兰空有中文文档很好搭建，官方宣传：半小时搭好)


# 安装
### 主要参考资料
非常感谢

1. [搭建 Lsky Pro 兰空图床](https://www.zatp.com/post/lsky-pro-image-hosting/)

2. [兰空图床搭建](https://blog.csdn.net/Bacon_Fish/article/details/125681902)

## 为啥不用宝塔面板
毕竟1G的机子跑宝塔完全没问题

但

[宝塔面板爆重大漏洞，数据库无鉴权直接访问](https://zhuanlan.zhihu.com/p/196684686)

在舍友的极力劝阻下我开始了我的苦闷的从0开始之旅

## 没头苍蝇阶段

所谓的半小时，我整了整整一天。

一开始按照中文文档搭建，几乎没任何指导，并且有nginx和php两大知识盲区，后来……

痛苦

直到我找到了上面引用的第2篇教程

## 安装Nginx
参阅[官方文档](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/)后

决定直接apt安装

以下均root用户命令

```bash
apt update
apt upgrade
apt install nginx
#查询其工作状态
systemctl status nginx
```
在浏览器内输入您的IP地址或域名并打开

显示：
![](https://euserver.1314171.xyz/i/2022/09/08/6319f88d6c9cb.jpg)
说明Nginx已经正常工作

## 安装PHP
根据官方的文档，要满足如下要求
    
    PHP >= 8.0.2
    BCMath PHP 扩展
    Ctype PHP 扩展
    DOM PHP 拓展
    Fileinfo PHP 扩展
    JSON PHP 扩展
    Mbstring PHP 扩展
    OpenSSL PHP 扩展
    PDO PHP 扩展
    Tokenizer PHP 扩展
    XML PHP 扩展
    Imagick 拓展
    exec、shell_exec 函数
    readlink、symlink 函数
    putenv、getenv 函数
    chmod、chown、fileperms 函数

有些头大
最后整理出来的安装命令如下：
```bash
curl -sSL https://packages.sury.org/php/README.txt | bash -x

#上述脚本内容为:
#!/bin/sh
# To add this repository please do:

#if [ "$(whoami)" != "root" ]; then
#    SUDO=sudo
#fi

#${SUDO} apt-get update
#${SUDO} apt-get -y install apt-transport-https lsb-release ca-certificates curl
#${SUDO} curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
#${SUDO} sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
#${SUDO} apt-get update

# 这里安装8.1版本
apt install -y php8.1 php8.1-cli php8.1-common php8.1-fpm php8.1-xml php8.1-curl php8.1-mysql php8.1-sqlite3 php8.1-mbstring php8.1-gd php8.1-fileinfo php8.1-exif php8.1-bcmath php8.1-imagick php8.1-opcache php8.1-readline php8.1-dom php8.1-tokenizer

apt install libssl-dev openssl
```

上述脚本将官方源添加到apt中，apt install完成了所有依赖的安装。

## 配置PHP
打开php.ini，示例命令
```bash
vim /etc/php/8.1/fpm/php.ini
#注意路径中的8.1改成您安装的对应版本号
```

在其中找到如下几点：
1. 找到`disable_functions`，若 “=” 右侧存在`exec、shell_exec、readlink、symlink、putenv、getenv`函数，将其删除（默认状态下，等号右侧为空白）；
2. 找到`memory_limit`，根据机器配置适当调大 “=” 右侧最大内存大小（默认php128mb内存）；
3. 找到`post_max_size`，适当调大 “=” 右侧POST方法所能传输数据的最大大小（这是队列大小，调整为想上传最大单个文件大小乘上想一次性上传图片数）；
4. 找到`upload_max_filesize`，适当调大 “=” 右侧最大文件上传大小（这是单个文件上传大小）；
5. `max_execution_time` 右侧为最大执行时间，默认为30秒，也就是说如果上传超过 30 秒，该队列就会停止
6. 找到`open_basedir`，在其前面加上“;"（默认已添加）。

重启php-fpm并检查工作状态
```bash
systemctl restart php8.1-fpm
#根据安装版本调整版本号
systemctl status php8.1-fpm
#根据安装版本调整版本号
```

## 安装兰空图床本体
1. 下载源码：
从[release](https://github.com/lsky-org/lsky-pro/releases)下载最新安装包，放在你想安装的路径上

这里以 `/home/www/lsky` 路径举例

```bash
#首先安装解压
apt install unzip
# 下一句注意修改版本号
unzip -d /home/www/lsky/ lsky-pro-2.1.zip
#将安装文件夹及其子文件夹权限设为755，所有者改为www-data：
chmod -R 755 /home/www/lsky
chown -R www-data /home/www/lsky
```
## 配置Nginx和PHP协同
打开default网站配置文件
```bash
vim /etc/nginx/sites-available/default
```
将内容复制到
`/etc/nginx/cinf.d`下新建一文件命名为：`lsky.conf`

修改其中
0. 去除掉80端口后的 default……
1. 转到server块，找到root项，将其后的路径指向Lsky Pro安装路径的public文件夹；
2. 找到index项，在其后添加index.php；
3. 找到server_name项，将其后的内容改为您的IP或域名；
4. 转到location / 块，找到try_files项，将 =404 改为 /index.php?$query_string（即设置伪静态）；
5. 转到location ~ \.php$块，去除行前#号，选择With php-fpm方法，将路径中的PHP版本修改为对应安装版本。修改完的效果应如图所示：

![](https://euserver.1314171.xyz/i/2022/09/08/6319f86f07b3e.png)

执行以下命令打开Nginx配置文档：

```bash
vim /etc/nginx/nginx.conf
```
在http块中添加
```json
client_max_body_size 25m;
#25m为Nginx限制的一次性上传文件最大大小
#大小可视情况调整
```

检查配置有无错误，重启
```bash
nginx -t
#若无错误
systemctl restart nginx
```
## 安装数据库
尝试安装MySQL

但官方源始终无法curl到，我也懒得整了

就用SQLite，简单不用安装
## 初始化图床
配置好域名以后，访问站点首页，程序会自动跳转至安装页面，环境检测通过以后即可通过引导进行安装。

`数据库名称/路径`留空即可

## 接入api和picgo协同
[参考这个博客设置请求](https://www.shejibiji.com/archives/8411)

但是捏，套了cdn的地址没法在线post,解了cdn之后才发现并不能post ipv6地址……纯ipv6的痛苦

想了想，发现能本地post，命令如下

```bash
curl localhost:80/api/v1/tokens -X POST -d 'email=example@example.com&password=yourpass'
```

可以正常返回
![成功！这就是我用picgo上传的图片](https://euserver.1314171.xyz/i/2022/09/08/6319f75d3ad36.png)
## 发现能用webdav等存储
还未尝试，TODO:

## 其他问题，http图床链接在vscode中无法加载预览解决

参看如下两篇就明白了

[markdown预览](https://blog.csdn.net/wejack/article/details/122309967?spm=1001.2101.3001.6650.5&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-5-122309967-blog-105007956.pc_relevant_aa_2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7ERate-5-122309967-blog-105007956.pc_relevant_aa_2&utm_relevant_index=6)

[加载http链接](https://blog.csdn.net/qq_41821678/article/details/105007956)

>本篇博客所有图片均上传在新部署的图床上

>目前图床关闭注册以及游客上传功能，没有公开计划，如有需要请联系我

# 其他友情链接
## nginx
[教程1](https://www.myfreax.com/how-to-install-nginx-on-debian-10/)

[教程2](https://www.myfreax.com/nginx-commands-you-should-know/)

## PHP
[PHP教程](https://blog.csdn.net/Time888/article/details/113935083)