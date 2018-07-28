---
title: "如何将网站加入Google搜索"
subtitle:    ""
description: "学习将新建的网站加入Google的搜索中。最近在学习使用hugo建自己的blog，我的建站经历可参考：通过 netlify 部署自动化 hugo 。建好之后发现通过Google无法搜索到自己的网站，这多没意思呀，于是又开始学习折腾怎么让Google能够搜到自己的网站。经过2天终于搞明白了，现在在Google上可以搜索到自己网站的内容了。HAPPY......."
date: 2018-07-28T10:15:45+08:00
author:      "Zhengx"
image:       ""
tags:        ["Google", "Tech"]
categories:  ["Tech" ]
published: true
showtoc: false 
---



最近在学习使用hugo建自己的blog，我的建站经历可参考：[通过 netlify 部署自动化 hugo](https://blog.ifyes.club/post/%E9%80%9A%E8%BF%87netlify%E9%83%A8%E7%BD%B2%E8%87%AA%E5%8A%A8%E5%8C%96hugo/) 。建好之后发现通过Google无法搜索到自己的网站，这多没意思呀，于是又开始学习折腾怎么让Google能够搜到自己的网站。经过2天终于搞明白了，现在在Google上可以搜索到自己网站的内容了。HAPPY.......

**LET GO**

1.首先需要登录[Google Search Console](https://www.google.com/webmasters/tools/home?hl=zh-CN&authuser=0) 将自己的网站地址添加上，点击添加属性按钮进行添加

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728103229.png)

2.在弹出的窗口输入需要加入的域名

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728103301.png)

3.接下来Google会验证我们加入的域名所有权，这个地方比较折腾我搞了很久才搞明白，因为它有很多方式来进行验证。包括了HTML文件上传、HTML标记、域名提供商、Google analytics、Google跟踪代码管理器。其中最方便的是通过域名提供商的方式进行验证。

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728103755.png)

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728103733.png)

4.登录自己的域名服务商，在DNS设置那边加入TXT记录就ok了，也可以通过添加CNAME记录的方式进行添加，我用的DNS服务商是[Dnspod](https://www.dnspod.cn/) ，在Google中没有默认列表，就选择了其他。我最后是通过添加CNAME记录的方式添加成功的，需要添加的内容为**CNAME 标签 / 主机** 和**CNAME 目的地 / 目标** 。在域名服务商那边将相关记录添加好了之后点击下方的验证就进入到下一步了。

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728104639.png)

5.如果不验证或验证失败，就会出现“您无权使用此资源。请验证此资源，或请资源所有者将您添加为用户。”，验证成功就可以进入控制台进行管理了。

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728105731.png)

6.进入网站的控制台之后，最重要的加入网站地址sitemaps.xml将网站的地图手动加入，这样可以加快将网站提交给Google，让Google能够尽快的搜索到自己的网站。添加的地方在“抓取-站点地图”点击右边的添加/测试站点地图。大部分blog如hexo和hugo都是支持sitemap.xml站点文件，位置一般在根目录下。添加成功之后，可以看到已经提交的网址数。

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180728110719.png)

到此结束，我已经搞定了将网站加入Google搜索，也行设定好之后不能马上搜索到，等一两天就ok了。Google加入网站的速度还是挺快的。