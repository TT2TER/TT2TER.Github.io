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

描述一下，注意网页的根目录和build command（一般command默认即可，根目录是生成网页的所有资源的根目录）

好了好了图床换了
详见：

<li><a href="/post/220903picture-server">尝试新的图床解决方案</li>

补个截图：
![](https://fastly.jsdelivr.net/gh/TT2TER/image1st@main/img/20220904001131.png)



# 把原来的域名改绑定

原来vercel绑定的改为`yournamebackup`

域名同样有https,但比vercel慢点，等等就行了

直接在域名解析CNAME到你的`yourproject.netlify.app`就行

# 补一手很漂亮的部署日志
```log
9:22:08 PM: Build ready to start
9:22:12 PM: build-image version: d7b3dbfb0846505993c9a131894d1858074c90b4 (focal)
9:22:12 PM: build-image tag: v4.10.1
9:22:12 PM: buildbot version: 67e75f1ba713a8213d4b5a8ccf9708af751e2390
9:22:12 PM: Fetching cached dependencies
9:22:12 PM: Failed to fetch cache, continuing with build
9:22:12 PM: Starting to prepare the repo for build
9:22:12 PM: No cached dependencies found. Cloning fresh repo
9:22:12 PM: git clone https://github.com/TT2TER/TT2TER.Github.io
9:22:14 PM: Preparing Git Reference refs/heads/source
9:22:14 PM: Parsing package.json dependencies
9:22:15 PM: Starting build script
9:22:15 PM: Installing dependencies
9:22:15 PM: Python version set to 2.7
9:22:15 PM: Downloading and installing node v16.17.0...
9:22:15 PM: Downloading https://nodejs.org/dist/v16.17.0/node-v16.17.0-linux-x64.tar.xz...
9:22:16 PM: Computing checksum with sha256sum
9:22:16 PM: Checksums matched!
9:22:19 PM: Now using node v16.17.0 (npm v8.15.0)
9:22:20 PM: Started restoring cached build plugins
9:22:20 PM: Finished restoring cached build plugins
9:22:20 PM: Attempting ruby version 2.7.2, read from environment
9:22:20 PM: Using ruby version 2.7.2
9:22:21 PM: Using PHP version 8.0
9:22:21 PM: No npm workspaces detected
9:22:21 PM: Started restoring cached node modules
9:22:21 PM: Finished restoring cached node modules
9:22:21 PM: Installing NPM modules using NPM version 8.15.0
9:22:21 PM: npm WARN config tmp This setting is no longer used.  npm stores temporary files in a special
9:22:21 PM: npm WARN config location in the cache, and they are managed by
9:22:21 PM: npm WARN config     [`cacache`](http://npm.im/cacache).
9:22:21 PM: npm WARN config tmp This setting is no longer used.  npm stores temporary files in a special
9:22:21 PM: npm WARN config location in the cache, and they are managed by
9:22:21 PM: npm WARN config     [`cacache`](http://npm.im/cacache).
9:22:23 PM: npm WARN deprecated source-map-url@0.4.1: See https://github.com/lydell/source-map-url#deprecated
9:22:23 PM: npm WARN deprecated source-map-resolve@0.5.3: See https://github.com/lydell/source-map-resolve#deprecated
9:22:23 PM: npm WARN deprecated source-map-resolve@0.6.0: See https://github.com/lydell/source-map-resolve#deprecated
9:22:23 PM: npm WARN deprecated nvm@0.0.4: This is NOT the correct nvm. Visit https://nvm.sh and use the curl command to install it.
9:22:24 PM: npm WARN deprecated hexo-bunyan@1.0.0: Please see https://github.com/hexojs/hexo-bunyan/issues/17
9:22:24 PM: npm WARN deprecated chokidar@2.1.8: Chokidar 2 does not receive security updates since 2019. Upgrade to chokidar 3 with 15x fewer dependencies
9:22:24 PM: npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
9:22:24 PM: npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
9:22:25 PM: npm WARN deprecated highlight.js@9.18.5: Support has ended for 9.x series. Upgrade to @latest
9:22:25 PM: npm WARN deprecated core-js@1.2.7: core-js@<3.23.3 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Some versions have web compatibility issues. Please, upgrade your dependencies to the actual version of core-js.
9:22:27 PM: added 535 packages, and audited 536 packages in 6s
9:22:27 PM: 25 packages are looking for funding
9:22:27 PM:   run `npm fund` for details
9:22:27 PM: 22 vulnerabilities (2 low, 6 moderate, 11 high, 3 critical)
9:22:27 PM: To address issues that do not require attention, run:
9:22:27 PM:   npm audit fix
9:22:27 PM: To address all issues possible (including breaking changes), run:
9:22:27 PM:   npm audit fix --force
9:22:27 PM: Some issues need review, and may require choosing
9:22:27 PM: a different dependency.
9:22:27 PM: Run `npm audit` for details.
9:22:27 PM: NPM modules installed
9:22:28 PM: npm WARN config tmp This setting is no longer used.  npm stores temporary files in a special
9:22:28 PM: npm WARN config location in the cache, and they are managed by
9:22:28 PM: npm WARN config     [`cacache`](http://npm.im/cacache).
9:22:28 PM: Started restoring cached go cache
9:22:28 PM: Finished restoring cached go cache
9:22:28 PM: Installing Go version 1.17 (requested 1.17)
9:22:34 PM: unset GOOS;
9:22:34 PM: unset GOARCH;
9:22:34 PM: export GOROOT='/opt/buildhome/.gimme/versions/go1.17.linux.amd64';
9:22:34 PM: export PATH="/opt/buildhome/.gimme/versions/go1.17.linux.amd64/bin:${PATH}";
9:22:34 PM: go version >&2;
9:22:34 PM: export GIMME_ENV="/opt/buildhome/.gimme/env/go1.17.linux.amd64.env"
9:22:34 PM: go version go1.17 linux/amd64
9:22:34 PM: Installing missing commands
9:22:34 PM: Verify run directory
9:22:35 PM: ​
9:22:35 PM: ────────────────────────────────────────────────────────────────
9:22:35 PM:   Netlify Build                                                 
9:22:35 PM: ────────────────────────────────────────────────────────────────
9:22:35 PM: ​
9:22:35 PM: ❯ Version
9:22:35 PM:   @netlify/build 27.16.1
9:22:35 PM: ​
9:22:35 PM: ❯ Flags
9:22:35 PM:   baseRelDir: true
9:22:35 PM:   buildId: 63135500d4077517d5f93a18
9:22:35 PM:   deployId: 63135500d4077517d5f93a1a
9:22:35 PM: ​
9:22:35 PM: ❯ Current directory
9:22:35 PM:   /opt/build/repo
9:22:35 PM: ​
9:22:35 PM: ❯ Config file
9:22:35 PM:   No config file was defined: using default values.
9:22:35 PM: ​
9:22:35 PM: ❯ Context
9:22:35 PM:   production
9:22:35 PM: ​
9:22:35 PM: ────────────────────────────────────────────────────────────────
9:22:35 PM:   1. Build command from Netlify app                             
9:22:35 PM: ────────────────────────────────────────────────────────────────
9:22:35 PM: ​
9:22:35 PM: $ npm run build
9:22:35 PM: npm WARN config tmp This setting is no longer used.  npm stores temporary files in a special
9:22:35 PM: npm WARN config location in the cache, and they are managed by
9:22:35 PM: npm WARN config     [`cacache`](http://npm.im/cacache).
9:22:35 PM: > hexo-site@0.0.0 build
9:22:35 PM: > hexo generate
9:22:35 PM: INFO  Validating config
9:22:35 PM: INFO  Start processing
9:22:36 PM: ERROR {
9:22:36 PM:   err: ValidationError: `null` is not a string!
9:22:36 PM:       at new WarehouseError (/opt/build/repo/node_modules/warehouse/lib/error.js:14:11)
9:22:36 PM:       at new ValidationError (/opt/build/repo/node_modules/warehouse/lib/error/validation.js:5:1)
9:22:36 PM:       at SchemaTypeString.validate (/opt/build/repo/node_modules/warehouse/lib/types/string.js:36:13)
9:22:36 PM:       at Array.<anonymous> (/opt/build/repo/node_modules/warehouse/lib/schema.js:510:27)
9:22:36 PM:       at Schema._applySetters (/opt/build/repo/node_modules/warehouse/lib/schema.js:640:15)
9:22:36 PM:       at _Model._insertOne (/opt/build/repo/node_modules/warehouse/lib/model.js:158:12)
9:22:36 PM:       at /opt/build/repo/node_modules/warehouse/lib/model.js:179:63
9:22:36 PM:       at tryCatcher (/opt/build/repo/node_modules/bluebird/js/release/util.js:16:23)
9:22:36 PM:       at /opt/build/repo/node_modules/bluebird/js/release/using.js:185:26
9:22:36 PM:       at tryCatcher (/opt/build/repo/node_modules/bluebird/js/release/util.js:16:23)
9:22:36 PM:       at Promise._settlePromiseFromHandler (/opt/build/repo/node_modules/bluebird/js/release/promise.js:547:31)
9:22:36 PM:       at Promise._settlePromise (/opt/build/repo/node_modules/bluebird/js/release/promise.js:604:18)
9:22:36 PM:       at Promise._settlePromise0 (/opt/build/repo/node_modules/bluebird/js/release/promise.js:649:10)
9:22:36 PM:       at Promise._settlePromises (/opt/build/repo/node_modules/bluebird/js/release/promise.js:729:18)
9:22:36 PM:       at Promise._fulfill (/opt/build/repo/node_modules/bluebird/js/release/promise.js:673:18)
9:22:36 PM:       at PromiseArray._resolve (/opt/build/repo/node_modules/bluebird/js/release/promise_array.js:127:19) {
9:22:36 PM:     code: undefined
9:22:36 PM:   }
9:22:36 PM: } Process failed: %s _posts/220705bashshell.md
9:22:37 PM: INFO 
9:22:37 PM: ------------------------------------------------
9:22:37 PM: |                                              |
9:22:37 PM: |     ________  __            _        __      |
9:22:37 PM: |    |_   __  |[  |          (_)      |  ]     |
9:22:37 PM: |      | |_ \_| | | __   _   __   .--.| |      |
9:22:37 PM: |      |  _|    | |[  | | | [  |/ /'`\' |      ||     _| |_     | | | \_/ |, | || \__/  |      |
9:22:37 PM: |    |_____|   [___]'.__.'_/[___]'.__.;__]     ||                                              |
9:22:37 PM: |             感谢使用 Fluid 主题 !            |
9:22:37 PM: |    文档: https://hexo.fluid-dev.com/docs/    |
9:22:37 PM: |                                              |
9:22:37 PM: ------------------------------------------------
9:22:37 PM: INFO  Files loaded in 1.38 s
9:22:37 PM: INFO  Generated: css/custom.css
9:22:37 PM: INFO  Generated: js/duration.js
9:22:37 PM: INFO  Generated: googlefae3894a3fd4fa2c.html
9:22:37 PM: INFO  Generated: baidusitemap.xml
9:22:37 PM: INFO  Generated: atom.xml
9:22:37 PM: INFO  Generated: sitemap.xml
9:22:37 PM: INFO  Generated: sitemap.txt
9:22:37 PM: INFO  Generated: local-search.xml
9:22:37 PM: INFO  Generated: about/index.html
9:22:37 PM: INFO  Generated: archives/index.html
9:22:37 PM: INFO  Generated: archives/2022/03/index.html
9:22:37 PM: INFO  Generated: archives/2022/04/index.html
9:22:37 PM: INFO  Generated: archives/2022/index.html
9:22:37 PM: INFO  Generated: archives/2022/05/index.html
9:22:37 PM: INFO  Generated: archives/2022/07/index.html
9:22:37 PM: INFO  Generated: archives/2022/08/index.html
9:22:37 PM: INFO  Generated: links/index.html
9:22:37 PM: INFO  Generated: post/220823alist.html
9:22:37 PM: INFO  Generated: tags/index.html
9:22:37 PM: INFO  Generated: 404.html
9:22:37 PM: INFO  Generated: categories/index.html
9:22:37 PM: INFO  Generated: post/220818blogtovercel.html
9:22:37 PM: INFO  Generated: post/220805sitemap.html
9:22:37 PM: INFO  Generated: post/220823proxytuic.html
9:22:37 PM: INFO  Generated: post/220809Docker-rss.html
9:22:37 PM: INFO  Generated: post/220819docsifyDeploy.html
9:22:37 PM: INFO  Generated: post/220715switchhost.html
9:22:37 PM: INFO  Generated: post/220807photosync.html
9:22:37 PM: INFO  Generated: post/220716visual-3.html
9:22:37 PM: INFO  Generated: post/220714NASandZSH.html
9:22:37 PM: INFO  Generated: post/220714hlink.html
9:22:37 PM: INFO  Generated: post/220709visual-2.html
9:22:37 PM: INFO  Generated: post/220706Jellyfin.html
9:22:37 PM: INFO  Generated: post/220705setting-qb-tr-IYUUplus.html
9:22:37 PM: INFO  Generated: post/220705tcp6-tcp4.html
9:22:37 PM: INFO  Generated: post/220518install.html
9:22:37 PM: INFO  Generated: post/220703nassystemfix.html
9:22:37 PM: INFO  Generated: post/220703rtmp.html
9:22:37 PM: INFO  Generated: post/220629networkProblem.html
9:22:37 PM: INFO  Generated: post/220531fixcdn.html
9:22:37 PM: INFO  Generated: post/220518nasbuy.html
9:22:37 PM: INFO  Generated: post/220517PREinstallNAS.html
9:22:37 PM: INFO  Generated: post/220518nasPlan.html
9:22:37 PM: INFO  Generated: post/220511ssh-connect-to-ssh-github.html
9:22:37 PM: INFO  Generated: post/220511sonic2.html
9:22:37 PM: INFO  Generated: post/TheWayToNAS.html
9:22:37 PM: INFO  Generated: post/220507get-news-efficiently.html
9:22:37 PM: INFO  Generated: post/220506feed-me.html
9:22:37 PM: INFO  Generated: post/220508picture-server.html
9:22:37 PM: INFO  Generated: post/220513DefensivePessimism.html
9:22:37 PM: INFO  Generated: post/0524UPDLinks.html
9:22:37 PM: INFO  Generated: post/220509freeipv6vps.html
9:22:37 PM: INFO  Generated: post/220417apprcn.html
9:22:37 PM: INFO  Generated: post/220426how-to-search-English-words.html
9:22:37 PM: INFO  Generated: post/0517UPDAphorisms.html
9:22:37 PM: INFO  Generated: post/220330a-network-problem-solve.html
9:22:37 PM: INFO  Generated: post/220327About-Learning-with-a-Video.html
9:22:37 PM: INFO  Generated: post/220326Reason-to-Learn-English.html
9:22:37 PM: INFO  Generated: post/220326hello-myblog.html
9:22:37 PM: INFO  Generated: post/TODOlist.html
9:22:37 PM: INFO  Generated: index.html
9:22:37 PM: INFO  Generated: post/220325codewithvscode.html
9:22:37 PM: INFO  Generated: img/avatar.png
9:22:37 PM: INFO  Generated: xml/local-search.xml
9:22:37 PM: INFO  Generated: post/220324firstblog.html
9:22:37 PM: INFO  Generated: archives/2022/page/2/index.html
9:22:37 PM: INFO  Generated: archives/2022/05/page/2/index.html
9:22:37 PM: INFO  Generated: archives/page/2/index.html
9:22:37 PM: INFO  Generated: page/5/index.html
9:22:37 PM: INFO  Generated: categories/学习过程/英语学习/index.html
9:22:37 PM: INFO  Generated: img/loading.gif
9:22:37 PM: INFO  Generated: img/fluid.png
9:22:37 PM: INFO  Generated: img/police_beian.png
9:22:37 PM: INFO  Generated: img/Ficon.png
9:22:37 PM: INFO  Generated: img/Wechat.jpg
9:22:37 PM: INFO  Generated: archives/page/4/index.html
9:22:37 PM: INFO  Generated: archives/2022/page/4/index.html
9:22:37 PM: INFO  Generated: archives/page/5/index.html
9:22:37 PM: INFO  Generated: categories/share/index.html
9:22:37 PM: INFO  Generated: archives/page/3/index.html
9:22:37 PM: INFO  Generated: archives/2022/page/3/index.html
9:22:37 PM: INFO  Generated: categories/idea/index.html
9:22:37 PM: INFO  Generated: archives/2022/page/5/index.html
9:22:37 PM: INFO  Generated: categories/Problems/index.html
9:22:37 PM: INFO  Generated: tags/network/index.html
9:22:37 PM: INFO  Generated: categories/学习教程/index.html
9:22:37 PM: INFO  Generated: categories/Diary/index.html
9:22:37 PM: INFO  Generated: tags/proxy/index.html
9:22:37 PM: INFO  Generated: tags/share/index.html
9:22:37 PM: INFO  Generated: tags/Test/index.html
9:22:37 PM: INFO  Generated: tags/vscode/index.html
9:22:37 PM: INFO  Generated: tags/github/index.html
9:22:37 PM: INFO  Generated: tags/English/index.html
9:22:37 PM: INFO  Generated: tags/Geography/index.html
9:22:37 PM: INFO  Generated: tags/Hexo/index.html
9:22:37 PM: INFO  Generated: tags/image/index.html
9:22:37 PM: INFO  Generated: tags/F1/index.html
9:22:37 PM: INFO  Generated: tags/video/index.html
9:22:37 PM: INFO  Generated: tags/font/index.html
9:22:37 PM: INFO  Generated: tags/ipv6/index.html
9:22:37 PM: INFO  Generated: tags/rss/index.html
9:22:37 PM: INFO  Generated: tags/information/index.html
9:22:37 PM: INFO  Generated: tags/blog/index.html
9:22:37 PM: INFO  Generated: tags/vps/index.html
9:22:37 PM: INFO  Generated: tags/Trojan/index.html
9:22:37 PM: INFO  Generated: tags/ilm/index.html
9:22:37 PM: INFO  Generated: tags/git/index.html
9:22:37 PM: INFO  Generated: tags/strategy/index.html
9:22:37 PM: INFO  Generated: tags/docker/index.html
9:22:37 PM: INFO  Generated: tags/ssh/index.html
9:22:37 PM: INFO  Generated: tags/pt/index.html
9:22:37 PM: INFO  Generated: tags/film/index.html
9:22:37 PM: INFO  Generated: tags/portainer/index.html
9:22:37 PM: INFO  Generated: tags/计算机视觉/index.html
9:22:37 PM: INFO  Generated: tags/shell/index.html
9:22:37 PM: INFO  Generated: tags/docsify/index.html
9:22:37 PM: INFO  Generated: tags/host/index.html
9:22:37 PM: INFO  Generated: tags/alist/index.html
9:22:37 PM: INFO  Generated: tags/tuic/index.html
9:22:37 PM: INFO  Generated: page/2/index.html
9:22:37 PM: INFO  Generated: tags/vercel/index.html
9:22:37 PM: INFO  Generated: page/3/index.html
9:22:37 PM: INFO  Generated: tags/HiHysteria/index.html
9:22:37 PM: INFO  Generated: tags/list/index.html
9:22:37 PM: INFO  Generated: page/4/index.html
9:22:37 PM: INFO  Generated: categories/教程/index.html
9:22:37 PM: INFO  Generated: categories/学习过程/index.html
9:22:37 PM: INFO  Generated: tags/nas/index.html
9:22:37 PM: INFO  Generated: categories/教程/page/2/index.html
9:22:37 PM: INFO  Generated: tags/nas/page/2/index.html
9:22:37 PM: INFO  Generated: css/highlight-dark.css
9:22:37 PM: INFO  Generated: css/gitalk.css
9:22:37 PM: INFO  Generated: js/boot.js
9:22:37 PM: INFO  Generated: js/color-schema.js
9:22:37 PM: INFO  Generated: css/highlight.css
9:22:37 PM: INFO  Generated: js/img-lazyload.js
9:22:37 PM: INFO  Generated: js/leancloud.js
9:22:37 PM: INFO  Generated: js/local-search.js
9:22:37 PM: INFO  Generated: js/plugins.js
9:22:37 PM: INFO  Generated: js/events.js
9:22:37 PM: INFO  Generated: js/utils.js
9:22:37 PM: INFO  Generated: css/main.css
9:22:37 PM: INFO  Generated: img/default.png
9:22:37 PM: INFO  Generated: img/Being-grey.png
9:22:37 PM: INFO  Generated: img/Beijing.png
9:22:37 PM: INFO  Generated: css/sarasa-mono-sc-regular.ttf
9:22:37 PM: INFO  146 files generated in 626 ms
9:22:37 PM: ​
9:22:37 PM: (build.command completed in 2.7s)
9:22:37 PM: ​
9:22:37 PM: ────────────────────────────────────────────────────────────────
9:22:37 PM:   2. Deploy site                                                
9:22:37 PM: ────────────────────────────────────────────────────────────────
9:22:37 PM: ​
9:22:37 PM: Starting to deploy site from 'public'
9:22:37 PM: Creating deploy tree 
9:22:37 PM: Creating deploy upload records
9:22:38 PM: 129 new files to upload
9:22:38 PM: 0 new functions to upload
9:22:38 PM: 0% complete
9:22:38 PM: 5% complete
9:22:38 PM: 10% complete
9:22:38 PM: 15% complete
9:22:38 PM: 20% complete
9:22:38 PM: 25% complete
9:22:38 PM: 30% complete
9:22:38 PM: 35% complete
9:22:39 PM: 40% complete
9:22:39 PM: 45% complete
9:22:39 PM: 50% complete
9:22:39 PM: 55% complete
9:22:39 PM: 60% complete
9:22:39 PM: 65% complete
9:22:39 PM: 70% complete
9:22:39 PM: 75% complete
9:22:39 PM: 80% complete
9:22:39 PM: 85% complete
9:22:39 PM: 90% complete
9:22:39 PM: 95% complete
9:22:40 PM: 100% complete
9:22:40 PM: Site deploy was successfully initiated
9:22:40 PM: ​
9:22:40 PM: (Deploy site completed in 2.1s)
9:22:40 PM: ​
9:22:40 PM: ────────────────────────────────────────────────────────────────
9:22:40 PM:   Netlify Build Complete                                        
9:22:40 PM: ────────────────────────────────────────────────────────────────
9:22:40 PM: ​
9:22:40 PM: (Netlify Build completed in 4.9s)
9:22:40 PM: Caching artifacts
9:22:40 PM: Started saving node modules
9:22:40 PM: Finished saving node modules
9:22:40 PM: Started saving build plugins
9:22:40 PM: Finished saving build plugins
9:22:40 PM: Started saving pip cache
9:22:40 PM: Finished saving pip cache
9:22:40 PM: Started saving emacs cask dependencies
9:22:40 PM: Finished saving emacs cask dependencies
9:22:40 PM: Started saving maven dependencies
9:22:40 PM: Finished saving maven dependencies
9:22:40 PM: Started saving boot dependencies
9:22:40 PM: Starting post processing
9:22:40 PM: Finished saving boot dependencies
9:22:40 PM: Started saving rust rustup cache
9:22:40 PM: Finished saving rust rustup cache
9:22:40 PM: Started saving go dependencies
9:22:40 PM: Finished saving go dependencies
9:22:40 PM: Post processing - HTML
9:22:41 PM: Build script success
9:22:43 PM: Uploading Cache of size 152.9MB
9:22:45 PM: Finished processing build request in 32.554939097s
9:22:46 PM: Post processing - header rules
9:22:46 PM: Post processing - redirect rules
9:22:46 PM: Post processing done
9:22:49 PM: Site is live ✨
```