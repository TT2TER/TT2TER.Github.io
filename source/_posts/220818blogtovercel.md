---
title: 220818blogtovercel
tags:
  - blog
  - vercel
categories: 教程
excerpt: 因为有服务需要部署在vercel上所以提前用我的博客迁移过来试试，同时vercel可以被搜索引擎爬取到,一举两得
date: 2022-08-19 00:19:30
---

# 部署过程
## 01注册！（之前我在整hexo评论的时候注册过了
（题外话：我当时整评论插件居然没有写一篇博客，令人震惊，看起来官方和网上的评论插件的使用教程非常完美我当时应该很顺利的整下来了，其实写博客这种事情，就是为了给自己看，最后不管是重新部署还是升级，都可以有个参考，同时也是成长的过程）

[vercel官网](https://vercel.com/)

在官网注册就好了，可以先绑定github,方便后续联动

### 这里放几个参考博客可以看看注册过程
[这篇教程适合于注册之后用vercel新建一个hexo博客](https://zhuanlan.zhihu.com/p/342790013)

[这个博客Ui很好看，但没啥内容](https://fmcf.cc/technology/400/)

## 02迁移

新建；
![](https://s2.loli.net/2022/08/18/fVqH3cIdhD7Ui9r.png)

选择hexo在的目录导入（注意这里的仓库不是hexo-github-deploy插件生成的静态html文件的main分支，需要有source分支将本地hexo源码上传）
![](https://s2.loli.net/2022/08/18/C3mPY56vHbQ9UnK.png)

设置好名字（建议简短，因为vercel生成的临时白嫖域名就是你的名字.vercel.app，当然也可以换自己的域名)
![](https://s2.loli.net/2022/08/18/3cHx8tiMDZfRsCQ.png)

直接部署即可
然后就部署成功了！

以后每次更新源码，只要审查preview能否正常使用并发布即可（应该有自动化流程）
![](https://s2.loli.net/2022/08/18/L9uamWKdzSUhA6J.png)

如果你把默认分支给改为你放源码的分支，这样就能触发上述描述的自动更新：
![](https://s2.loli.net/2022/08/19/7oP1tfkAVlEZpSM.png)

## 03关于域名.html后缀的解决办法

```
<li>< a href="/post/220518nasPlan"  tags="">我想拿nas干点啥，以及我的后路</li>
```

在我的博客中类似这样的html语法的链接，在vercel中不能直接跳转到220518nasPlan.html,导致无法载入正常的网页

### 解决问题
通过和舍友交流，以及我的检索，我找到了如下博客

[我真的不想要.html](https://blog.ccknbc.cc/posts/i-dont-really-want-html/)

这里面给指明了原因和解决问题方向

> 在路由表默认逻辑上，Vervel,Gitlab,一致,Github,Gitee``Coding,Netlify一致…… ……用户可以在链接后加上.html则可正常访问相应内容

在文章中指出路由表vercel和github默认选项不同

他给出的解决办法是更改（新建）项目源码中Vercel.json，配置Routes

但现在这个方法官方不推荐，过时了

查看官方文档，找到

![](https://s2.loli.net/2022/08/18/AMyiCmXNJRdOvDW.png)
这里仅通过简单的设置即可将默认改成和github相同形式

[vercel官方文档](https://vercel.com/docs/project-configuration#project-configuration/clean-urls)

大功告成！

## 04将域名从github上改绑到vercel上

![](https://s2.loli.net/2022/08/18/ABek2L61JZWo5Nr.png)
在github上remove掉

![](https://s2.loli.net/2022/08/18/DeLNrVj1O2G597F.png)

直接添加域名，会发现
![](https://s2.loli.net/2022/08/19/79zMtFxpAb4jgB6.png)

因此要按照提示在cloudflare（或者你自己的域名解析商）改掉对应域名的CNAME解析由
![](https://s2.loli.net/2022/08/18/akZr1FY6SlqUoec.png)
改成
```
cname.vercel-dns.com
```
![](https://s2.loli.net/2022/08/19/Z29y3GBYDvTlN1p.png)

然后在vercel中改域名即可
![](https://s2.loli.net/2022/08/19/x2DQIXGgU4acJ68.png)

而且惊喜的发现，有Let's Encrypt的证书！

![](https://s2.loli.net/2022/08/19/H1Yu5W6ClnEbNBQ.png)

至此，迁移完成。检查各项功能正常。

# 一些感受

千万不要害怕阅读英文文档，克制自己全网页翻译的坏习惯，可以部分不确定的句子单独翻译，锻炼自己的英文阅读能力


