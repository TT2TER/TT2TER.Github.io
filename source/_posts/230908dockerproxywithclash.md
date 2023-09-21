---
title: 大三前三周（小学期）周报
tags:
  - Weekly Report
  - clash
  - proxy
  - Docker
categories:
  - Diary
  - 教程
excerpt: 记述一下小学期的代码实践，记录一下一次长达一天的docker代理相关的摸索
date: 2023-09-21 19:35:11
---

# 大三第一二周周报
总之这两周就是疯狂敲代码

写了一个即时通讯软件，代码见[github](https://github.com/TT2TER/Echoplex)

最大的感想就是前后端的配合如果没有提前沟通好接口，那就是灾难

我在项目中全权负责Qt界面，同时因为需要和客户端配合，所以也参与了客户端的一些开发，尤其是接口部分。

由于大家都是第一次写程序，所以有很多地方都没有提前预估好，比如在实现文件发送功能的时候，接口消息格式不是很全，导致界面没法按照
预想显示进度条和消息，这本来是一个很好解决的问题，但当时大家都很着急，于是几乎重写了整个消息头的参数（虽然改起来很好改，但是还是很麻烦）

Qt界面其实很简单，但是美化我一直没有涉猎到精髓，感觉这一块确实还可以继续探索，消息框和聊天气泡都是扁平化的风格，其他按键不是很完美。

就这样吧，没什么别的事情了

# 大三第三周周报
第三周是并行编程，还可以，事情不多，于是就有时间折腾点其他的……
## Docker摸索，为nas配一个clash代理
### 先说起因
- 上课发现自己的图床服务器忘了续费已经停机了，匆匆忙忙续费。6欧每年真的实惠，还好数据什么的服务商还都给保留着，要不然真的是鸡飞狗跳的一天了
    - 这里给自己加个todo，服务器只有10G空间，现在用了5G了，图床虽然占不了很大空间，但如果以后要换服务商，暂时还没有学习如何迁移图床，另外可能的话数据放nas上是最好的。
- 然后突然想起来之前自己想selfhost一个类似[pocket](https://getpocket.com/home)的稍后阅读书签和浏览器快照存档的东西。这个在 <li><a href="/post/2023week1"  tags="">第一周周报</li> 

- 中提到过。既然恰好没啥事情，就搭建一个吧
- 然后在当时找到的四个比较符合要求的里面找了一个ui最好看的（这里巨大伏笔，小丑的源头

### 我看上了linkwarden

先放链接：[linkwarden](https://github.com/Daniel31x13/linkwarden)
#### build无法连接网路
当时首先的想法是在nas上部署这个服务，从文档看，需要自己在本地从Dockerfile开始build主程序，同时dockerhub上别人构建好的也没说怎么用（当然现在我会用了）。nas被阉割了git，所以将文件拷贝到nas上，正常使用docker-compose up来运行，发现卡死在了

```Dockerfile
RUN yarn
```

这一步，报错内容是

```bash
 => => # yarn install v1.22.19                                                  
 => => # [1/4] Resolving packages...                                            
 => => # [2/4] Fetching packages... 
```

总之是因为网路问题导致无法连接下载所需要的node包吧，当时我的nas是没代理的，我寻思着，那就去在我电脑ubuntu双系统中去build完再想办法传给nas运行呗

#### Ubuntu也不能连接网路
双系统没有安装docker，重新装，还是没用搭理docker desktop，直接装engin。

- 题外话：在装compose的时候发现，现在已经不建议单独安装docker-compose了。也就是说docker-compose命令将成为过去时，以后会被plugin版本的docker compose完全替代

笑死，也连不上网是显而易见的，肉身在哪，网就在哪。

但能够尝试配置代理

这个坑尝试填了一下，把新下的docker的配置文件整的千疮百孔（不是）依旧卡在那一步。（现在来看应该只需要仔细阅读文档然后配置好build步骤的代理就行了，TODO:

当时没整成，又尝试去改Dockerfile文件里的命令，FROM RUN CMD啥的都了解了一下，在这里尝试加代理的环境变量，尝试给yarn换国内镜像源，无解（也许是因为docker千疮百孔了。

#### 退一步，也没有海阔天空
既然是国内网络问题，那就用vps build，然后……卡在了更早的一步，还不如本地跑的进度好，我也懒得去解决依赖的问题。

转头又去dockerhub上认真看了看其他人构建好的镜像，发现有个国人[老苏](https://laosu.cf/)十几天前构建的镜像虽然还没介绍怎么用，但也写明白了镜像构建过程，可以直接拿来用的单独的image...(只可惜一开始我既不懂docker build命令，也不懂docker image 和layer 以及stack的关系，反正就是之前不会用人家构建好的镜像)，但在这个时间点折腾过之前的东西之后我才能看明白，也才有机会自己写compose配置

镜像链接:[wbsu2003/linkwarden](https://registry.hub.docker.com/r/wbsu2003/linkwarden)
其中详细记述了构建过程

```bash
# 下载代码
git clone https://github.com/linkwarden/linkwarden.git

# 或者加个代理
git clone https://ghproxy.com/github.com/linkwarden/linkwarden.git

# 进入目录  
cd linkwarden

# 构建镜像
docker build -t wbsu2003/linkwarden:v1 .
```
#### 跑起来程序之后，才后知后觉意识到docker里面依旧访问不了外网

自己写照着文档写docker-compose.yml，配合上数据库，在双系统ubuntu跑起来了

发现只能快照百度等国内网站，不能对google，github等不存在的网站进行快照

在此前已经见识过代理配置的复杂，更何况最后这个项目不能部署在笔记本上，要不就是nas，要不就是vps

于是转战vps

#### vps一点空间没有
这个逆天玩意儿build完的镜像加起来有2个多g，之前提到的剩余空间已经不够了

不够先pull下压缩包再解压的空间，于是在vps上构建的这条路走不通了

### 看向定制系统的nas，硬着头皮去解决在docker里面弄一个clash以及其他docker链接这个clash

现在看在解决这个问题的时候，很多疑惑都受限于自己本身的能力限制理解不了报错，找不到问题原因，筛选不出正确的解决办法。

如果我对操作系统或计算机网络有更深的理解，可能问题会少很多。

在和Google以及gpt的激情交流下，我最后终于让服务在nas上跑起来了

#### 先跑clash
用的是dreamacro/clash:latest镜像

要把7890-7891代理的端口和9090ui面板的端口分别绑定到主机(如果不需要宿主机访问clash，就不用绑定代理的端口)

将配置文件绑定到/root/.config/clash/config.yaml，配置文件从电脑拷贝就行，奇怪的是我直接拷贝的文件clash不识别，但是我打开配置全选拷贝内容就可以

这一步参考的一些教程
[参考1](https://fugary.com/?p=363)
[参考2](http://www.qince.net/dockery7t0.html)

然后用nas自己的代理，设置到绑定的clash的端口，在nas终端中运行wget google.com，成功！说明clash在nas里跑起来了

#### 得让容器之间互相通信
凭借着前世对docker网络的一点点理解，我知道在同一个network下docker自动有一个类似dns的东西能直接将容器名解析为容器在network下的地址

所以大概的思路就出来了

即，让linkwarden，数据库，clash写在同一个docker-compose文件中

中间疑惑了半天代理应该怎么配置，如果之前对环境变量的理解深一点，就不会像现在这样狼狈

先贴上最后的docker-compose文件吧

```yaml
version: "3.5"
networks:
  my_network:
    driver: bridge

services:
  postgres:
    image: postgres
    env_file:
      - .env
    restart: always
    networks:
      - my_network
    volumes:
      - ./postgres:/var/lib/postgresql/data

  linkwarden:
    image: wbsu2003/linkwarden:latest
    env_file:
      - .env
    environment:
      - DATABASE_URL=postgresql://postgres:${POSTGRES_PASSWORD}@postgres:5432/postgres
      - http_proxy=http://clash_linkwarden:7890
      - https_proxy=http://clash_linkwarden:7890
    restart: always
    ports:
      - 0000:3000
    volumes:
      - /your_path/data:/data/data
    depends_on:
      - postgres
      - clash_linkwarden
    networks:
      - my_network
    dns:
      - 8.8.8.8

  clash_linkwarden:
    image: dreamacro/clash:latest
    restart: always
    ports: 
      - 0000:7890
      - 0000:7891
      - 0000:9090
    volumes:
      - /your_path/clash/config.yaml:/root/.config/clash/config.yaml
    networks:
      - my_network
    dns:
      - 8.8.8.8 
```

其中$.env$里放的是linkwarden官方要求的一些环境变量，放在和compose.yml同目录下

说一下里面的一些坑和仍未解决的问题吧

1. network自己新建，也可以不，compose会自动为里面的所有应用新建一个network
2. $- http_proxy=http://clash_linkwarden:7890 - https_proxy=http://clash_linkwarden:7890$ 这两句环境变量，用名称clash_linkwarden直接找到clash，此外，端口用clash原本的端口，而不是绑定之后的主机的端口，因为在这个网域下，其他容器对clash访问是直接的。同时，要用$http\_proxy$和$https\_proxy$而不是$HTTP\_PROXY$和$HTTPS\_PROXY$,这里environment:里的环境变量，就是容器中env命令显示出来的环境变量。

未解决的问题：
1. clash每次启动都需要设置allow lan?不确定，还没测试。如果需要好像得写在comfig.yaml里
2. 某些链接会出现以下报错```TypeError: fetch failed
 at Object.fetch (node:internal/deps/undici/undici:11576:11)
 at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
 at async imageOptimizer (/data/node_modules/next/dist/server/image-optimizer.js:521:29)
 at async cacheEntry.imageResponseCache.get.incrementalCache (/data/node_modules/next/dist/server/next-server.js:414:72)
 at async /data/node_modules/next/dist/server/response-cache/index.js:99:36 {
    cause: ConnectTimeoutError: Connect Timeout Error
   at onConnectTimeout (node:internal/deps/undici/undici:8522:28)
   at node:internal/deps/undici/undici:8480:50
   at Immediate._onImmediate (node:internal/deps/undici/undici:8511:13)
   at process.processImmediate (node:internal/timers:478:21) {
 code: 'UND_ERR_CONNECT_TIMEOUT'
    }
  }```
3. 一些复杂域名好像没法解析，比如像github某个仓库的一个界面。这里我尝试 配置了dns地址，但没有用，应该是2.这里的同源问题
4. 跨network域访问docker中clash，以解决现在把docker莫名的放在了其他服务的compose里，而且这种解决办法以后每次有应用需要代理，就得新启动一个clash docker，多少有点离谱

此外就是一些小细节

1. ui的界面可以使用公共的[http://yacd.haishan.me](http://yacd.haishan.me)，填写你的域名以及绑定在9090的实际的端口，在上面的例子里就是0000（笑死，上面所有0000都要替换一个空的端口。
2. 不知道为什么nas配置了代理之后上面ui界面等就会都走代理，而不是直接访问nas，因此这一块还得再研究怎么不冲突（其实nas暂时还没有用代理的需求，软件都是docker部署的。
3. 此外就是可以不用端口转发绑定ipv6的外网访问，可以用
```bash
socat TCP6-LISTEN:0000,ipv6-v6only=1,reuseaddr,fork TCP4:127.0.0.1:0000
```

但这个只能在当前窗口启动时使用，解决以及开机自启动详见：

<li><a href="/post/220705tcp6-tcp4"  tags="">IPV6访问NAS中Docker的服务</li> 



## copilot搭配vscode
```
[ERROR] [default] [2023-09-10T09:55:28.610Z] GitHub Copilot could not connect to server. Extension a……
```
配置代理就好了
https://docs.github.com/zh/copilot/configuring-github-copilot/configuring-network-settings-for-github-copilot