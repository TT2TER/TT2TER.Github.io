---
title: 我想拿nas干点啥？以及我的后路
tags: 
- nas
categories:
  - - 教程
  - - 学习过程
excerpt: 简单介绍一下我决定购买nas的原因，其实也是梳理一下大学以来的折腾历程
date: 2022-05-18 01:41:34
---

# 接触
来到了大学认识了一个喜欢折腾的舍友煎包，他看我喜欢看电影看电视剧，给我拉进了pt圈（私有种子，与bt协议相同，但……具体百度贴吧自行检索）

在pt圈nas是很好的低功耗下载种子的机器，同时也是很好的存储，流媒体播放设备。当时舍友对我说，整个nas，自己攒一个，便宜，用开源的FreeNas系统。这是初识。但当时由于我的需求过于单一（仅有pt这一个理由使用nas），资金不够（如果买成品nas），自己知识不够显然不能折腾（自己攒nas），所以就没有行动。

此后我的发展走了两条路线，技术路线和娱乐路线，最终殊途同归……

# 无意的发展终究引我来到了Nas的面前
在这之后，我由于学习需要，开始接触GitHub，Linux系统。在接触Linux初期萌生了整个硬件设备学习Linux的想法，当时的方案是买个低功耗小主机，也就是NUC。当时看上了一款英特尔的NUC（NUC8i3bek)，因为型号停产以及原价超出预算，我寻求了海鲜市场（咸鱼）帮助。找到了标价1350的机器，因为出价太低（950），卖家直接回绝，并多问了一句我打算拿他干啥，遂告知需求。卖家认为没必要上NUC，给我指了条路，用小容量固态装到移动硬盘盒里安装Linux。这条折腾硬件初体验以100元固态和硬盘盒为结果结束了。（虽然装完系统就没再研究）。如果当时买了NUC一定没有现在Nas什么事情了。在这之后，我尝试自己整自己的工作流，利用学校千兆大内网的优势，整了平板连接电脑的远程桌面，以及文件同步（VerySync)。这是技术路线初期的发展。

同期，我的娱乐路线也不消停。有了高码率高分辨率以及HDR资源稳定来源，带来的后果就是本地储存空间不够了。于是先后入手西数移动硬盘两块，分别是2tb和5tb。显然，越来越大的储存空间需求说明我的仓鼠党潜力被激发了。同时巨大的下载量让我每月校园网流量迅速耗尽到限速。在大一下半学期开学时期限速突然严格，限速后浏览网页都卡顿，让我重新想起之前还是那个舍友提到的校园网ipv6免流，遂开始折腾服务器，见
<li><a href="/post/220509freeipv6vps">校园网通过IPV6代理实现免流且顺利浏览谷歌学术和GitHub</li></a>
(因为之前用的代理机场只有ipv4而且根本找不到支持ipv6的代理机场，被迫自己搭建)
同时虽然上半学期也用免费的服务器学过如何搭建，但奈何免费，速度质量远不及要求，我就认为自己搭建这条路走不通。但现在需求来了，不得不硬头皮上，花钱买了服务器，用上了之前白嫖的域名。由此我真正拥有了自己的服务器。

在这之后，我又因为服务器和朋友搭了博客萌生了建站的想法，见
<li><a href="/post/220326hello-myblog">我的建站过程</li></a>
由此熟悉了命令行操作界面，同时在和其他同学交流中发现自己的折腾能力有了很大提高，不论是官方文档阅读，操作，解决问题方面。在五一假期写了第一篇从头到尾非常完整的技术类博客，也就是上文提到的ipv6免流，让我又对自己更有信心了。这是我技术路线的进一步发展。

在娱乐路线上，扫清了储存和网络（流量计量）方面的障碍，可谓是一马平川。我看着笔记本2k小屏幕和动辄几十个G的原盘发呆，萌生了买显示器的想法。一通挑选，选了（LG 27UL650）4k 加HDR400，以2000价格淘宝淘来了原价2700的显示器，屏幕大了敲代码也舒服了，随后键鼠也简单的升级了一下，同时外置了2.1声道音响。宿舍娱乐办公环境可以说极致性价比的顶配了。

到这里，娱乐需求和技术需求交汇了……

# 再识nas
到这里我已经有了基本的网络知识和硬件知识，有了些分享资源，备份数据的需求，舍友（又是他）给我推荐网盘本地挂载，我一瞅，太依赖网络环境，网盘没在手里也不放心。兜兜转转发现Nas竟然能满足我现有的需求，并且可能促进未来技术上的学习（毕竟手头有硬件能实践比什么都强）。

一条条捋刚刚提到的现有服务的技术问题
1. Linux 移动硬盘还是太费劲；Nas天然的Linux系统，而且对Linux虚拟机达到硬件级别的支持
2. 文件同步(VerySync),需要同步时电脑处在开机状态；nas功耗低而且就是为了7*24小时服务运作
3. pt下载，同上
4. 存储空间小；一般4盘位nas最多兼容16*4T
5. 分享文件，外网访问等影音需求；成型的解决方案，HDMI输出。

一一都能被nas提升服务质量

同时我还有了整影音中心，个人图书馆的想法。还有希望能让家里的父母随时备份手机里的照片，并且能在电视上实时观看高码率电影和电视剧。最后，还想让以后的课余生活有个支点，能学点东西（如Docker）。nas的需求逐渐清晰。

# 后路
最后促成购买的，是几乎没有的后顾之忧，nas近些年一直在涨价，二手机保值率很高，大不了没需求海鲜市场出掉，甚至可能赚钱。硬盘舍友能接盘（其实留着自己用也不会亏）。于是，它来了。

---
<li><a href="/post/TheWayToNAS">返回TheWayToNAS系列目录</li></a>