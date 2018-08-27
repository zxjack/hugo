---
title: "Picgo"
subtitle:    "非常好用的markdown图床工具"
description: "今天再找图床的时候发现了个非常好用的图床工具：picgo，它支持绝大部分的图床包括腾讯云、七牛、阿里云、github、又拍云、sm.ms、Imgur、微博等。而且是macOS、linux和windows64都支持。必须试着用用看。
官方链接为：https://github.com/Molunerfinn/PicGo
我在windows10下试着用了一下，直接下载windows版本安装就ok了。唯一麻烦一点的是图床的配置方面，不过有比较详细的文档跟着做就OK了。"
date: 2018-07-24T23:57:05+08:00
author:      "Zhengx"
image:       ""
tags:        ["Tech", "tools"]
categories:  ["Tech" ]
published: true
showtoc: false
---



写在前面：

今天再找图床的时候发现了个非常好用的图床工具：**picgo**，它支持绝大部分的图床包括腾讯云、七牛、阿里云、github、又拍云、sm.ms、Imgur、微博等。而且是macOS、linux和windows64都支持。必须试着用用看。

官方链接为：https://github.com/Molunerfinn/PicGo

我在windows10下试着用了一下，直接下载windows版本安装就ok了。唯一麻烦一点的是图床的配置方面，不过有比较详细的文档跟着做就OK了。

# 详细窗口的使用:

## 打开详细窗口

右键点击 menubar 图标可以找到打开详细窗口的菜单。

## 基本操作预览

![2017-12-09 00 13 05-min](https://user-images.githubusercontent.com/12621342/34242857-d177930a-e658-11e7-9688-7405851dd5e5.gif)

## 上传区

上传区支持拖拽上传或者点击区域打开文件夹上传

## 相册区

支持查看你上传成功的所有图片。点击图片可以预览。点击图片下面的图标可以复制链接或者删除图片（只是删除本地数据，使其不在相册区里出现）

### 支持编辑相册的图片信息（v1.5)

有些时候可能上传的图片的 url 事后需要更改，比如修改 http 到 https，比如加上一些操作后缀（例：七牛图床支持的 `?imgslim`）等等。PicGo 本次的更新也让你能够更方便地管理你的图片库。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/picgo_edit_info.gif)

## 微博图床

![image](https://user-images.githubusercontent.com/12621342/34974486-482c0caa-fac8-11e7-963b-8e0ee5418828.png)

上传的图片不会出现在你的微博相册里。可以选择链接的图片质量，这样在复制到剪贴板里的图片将会对应修改成对应的链接地址。设置你的微博图床可以选择两种模式：

1. 只需填写你的微博用户名密码即可。**缺点**：上传速度会慢（尤其 windows 平台），因为要经过很多层验证。并且如果出现需要验证码的情况无法解决。
2. 只需 Cookie 上传（PicGo v1.3.2 及以上版本支持）。切换成 cookie 模式。然后先登录[微博](https://weibo.com/)（必须先登录），之后打开 [minipublish 页面](https://weibo.com/minipublish)，如果你是 mac 用户，使用 `command+alt+i`，如果你是 windows 用户，使用 `F12` 打开控制台，选择 `Network` 标签栏。然后刷新一下页面，找到 Network 里的 `minipublish` 一项，再找到 `minipublish` 右侧的 `Cookie` 一项，把 `Cookie` 冒号后的值全部复制（不要把 `Cookie:` 这个也复制了）然后填入 `PicGo` 里的 Cookie 一栏。这样就行了。

![cookie](https://user-images.githubusercontent.com/12621342/34974243-fa5d2bf4-fac6-11e7-9869-a6a6e126cd15.png)

## 七牛图床

![image](https://user-images.githubusercontent.com/12621342/34243072-191cc4ae-e65a-11e7-99f6-ebe6b7dcaf86.png)

对应的密钥信息需要到七牛自己的控制台里找到。其中需要注意的是，自己的存储空间的区域需要确定：

![image](https://user-images.githubusercontent.com/12621342/34243146-69af085a-e65a-11e7-965c-2a3d15856480.png)

设定上传地址是指七牛云自动分配给你的网址，或者是你自己绑定的域名：

![image](https://user-images.githubusercontent.com/12621342/34245183-c38d9766-e663-11e7-964e-2d7a9ab9e9e9.png)

网址后缀通常是你用到了七牛的图片处理工具的时候会用到的一些处理参数。

## 腾讯云 COS

> 从 PicGo v1.5 版本开始，支持 COSv4 和 v5 版本。

### V4 版本说明

v4 版本是这个：

![image](https://user-images.githubusercontent.com/12621342/35483306-5e7ed570-047b-11e8-95a9-d56a3b4d2ba9.png)

需要登录腾讯云控制台。打开[密钥管理](https://console.qcloud.com/cos4/secret)

![image](https://user-images.githubusercontent.com/12621342/34243294-082c97cc-e65b-11e7-9412-dbc86433a91d.png)

按照对应的提示找到自己的 `APPID`、`SecretId`、`SecretKey`。

存储的空间名是你的 bucket 名字。

存储的区域需要额外注意，请到 bucket 列表里打开需要上传的 bucket 空间，然后如图可以看到对应的区域以及区域代码，比如我的是 `tj`：

![image](https://user-images.githubusercontent.com/12621342/34243443-befa715e-e65b-11e7-8404-aa5b8938a82b.png)

对应的区域代码如下：

![image](https://user-images.githubusercontent.com/12621342/34243476-edcc7798-e65b-11e7-8d59-8714cd0a59aa.png)

如果你想把图片上传到你的 bucket 空间的某个文件夹下，则需要在 PicGo 里的`指定存储路径`里加上你的文件夹路径。比如 `temp/`（注意一定要加 `/`）

### V5 版本说明

**1. ** 获取你的 APPID、SecretId 和 SecretKey

访问：<https://console.cloud.tencent.com/cam/capi>

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/get_key_id_secret.png)

**2. ** 获取 bucket 名以及存储区域代号

访问：<https://console.cloud.tencent.com/cos5/bucket>

创建一个存储桶。然后找到你的存储桶名和存储区域代号：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/get_bucket_area.png)

v5 版本的存储桶名称格式是 `bucket-appId`，类似于 `xxxx-12312313`。存储区域代码和 v4 版本的也有所区别，v5 版本的如我的是 `ap-beijing`，别复制错了。

**3. ** 选择 v5 版本并点击确定

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/choose_v5.png)

然后记得点击`设为默认图床`，这样上传才会默认走的是腾讯云 COS。

## 又拍云

![image](https://user-images.githubusercontent.com/12621342/34319574-a6e141d0-e820-11e7-9b20-0ec0eb9b36af.png)

![image](https://user-images.githubusercontent.com/12621342/34319588-01510cd6-e821-11e7-9eeb-e61265af53ad.png)

存储空间名即为你的服务名，加速域名即为你又拍云分配给你的域名或者是你自己绑定的域名。请注意，加速域名需要加 `http://` 或 `https://`。

![image](https://user-images.githubusercontent.com/12621342/34319600-656c8d80-e821-11e7-8b02-34aa31a2d53a.png)

操作员即为你自己为该存储空间设定的操作员名，密码即为对应的密码。

![image](https://user-images.githubusercontent.com/12621342/34319609-9fb3307a-e821-11e7-9746-b2e82417ba7f.png)

网址后缀为你针对图片进行的一些处理参数。

由于又拍云官方没有对云存储有一个直观的控制面板，所以推荐可以采用第三方 web 面板来查看和操作：

[又拍云存储 Web 版操作工具](https://github.com/xcuts/UPYUN-API-Web-Tool)

## GitHub 图床

**1. ** 首先你得有一个 GitHub 账号。注册 GitHub 就不用我多言。

**2. ** 新建一个仓库

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/create_new_repo.png)

记下你取的仓库名。

**3. ** 生成一个 token 用于 PicGo 操作你的仓库：

访问：<https://github.com/settings/tokens>

然后点击 `Generate new token`。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/generate_new_token.png)

把 repo 的勾打上即可。然后翻到页面最底部，点击 `Generate token` 的绿色按钮生成 token。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/20180508210435.png)

** 注意：** 这个 token 生成后只会显示一次！你要把这个 token 复制一下存到其他地方以备以后要用。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/copy_token.png)

**4. ** 配置 PicGo

** 注意：** 仓库名的格式是`用户名/仓库`，比如我创建了一个叫做 `test` 的仓库，在 PicGo 里我要设定的仓库名就是 `Molunerfinn/test`。一般我们选择 `master` 分支即可。然后记得点击确定以生效，然后可以点击`设为默认图床`来确保上传的图床是 GitHub。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/setup_github.png)

至此配置完毕，已经可以使用了。当你上传的时候，你会发现你的仓库里也会增加新的图片了：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/success.png)

## 阿里云 OSS

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/aliyun.png)

首先先在阿里云 OSS 的[控制台](https://usercenter.console.aliyun.com/#/manage/ak)里找到你的 `accessKeyId` 和 `accessKeySecret`：![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/aliyun-key.png)

创建一个 `bucket` 后，存储空间名即为 `bucket`:

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/aliyun-bucket.png)

确认你的[存储区域](https://www.alibabacloud.com/help/zh/doc-detail/31837.htm?spm=a2c63.p38356.a3.3.179112f0PBtYui)的代码：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/aliyun-area.png)

也可以在 bucket 页面找到：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/aliyun-bucket-2.png)如上图，存储区域就是 `oss-cn-beijing`

存储路径比如 `img/` 的话，上传的图片会默认放在 OSS 的 `img` 文件夹下。注意存储路径一定要以 `/` 结尾！存储路径是可选的，如果不需要请留空。

## Imgur

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/imgur-option.png)

登录 Imgur 后，在[此处](https://api.imgur.com/oauth2/addclient)生成你的 ClientId，记得选第二项，不需要 callbackurl 的。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/imgur-clientid.png)

于是你可以拿到你的 clientId:

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/imgur-client-id-2.png)

**注意**：imgur 貌似对中国大陆的 IP 和请求做出了限制，所以如果 clientId 没错的情况下无法上传图片的时候，可以考虑配置代理设置。默认只支持 HTTP 代理。如果觉得设置麻烦的可以考虑使用 SM.MS 图床。

------

## PicGo 设置

### 自定义快捷键

PicGo v1.4.0 版本开始支持自定义快捷键（默认快捷键是 `Cmd+Shift+P`【Mac】或者 `Ctrl+Shift+P`【Windows】），点击侧边栏 PicGo 设置选中修改快捷键：

![image](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/change-quick-key.png)

在打开的 dialog 里，点击 input 框，然后按下你想要的快捷键（也可以是组合键）。然后点击**确定保存**（否则不生效！）

![image](https://user-images.githubusercontent.com/12621342/35553216-ea22e18c-05d1-11e8-8913-047047b92c09.png)

### 自定义链接格式

PicGo 预置的有四种链接格式：`Markdown``HTML`\`URL`\`UBB`。如果你都不喜欢，想要自定义链接格式，可以选择`Custom`，然后在PicGo设置里点击`自定义链接格式 `，然后你可以配置自己想要的复制的链接格式。

![image](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/custom.png)

### 开关更新助手

PicGo 每次启动的时候会去检查最新版本。如果当前版本低于最新版本会提示你更新。如果你不想接到这条消息，那么可以在 PicGo 设置里把`打开更新助手`这个选项关闭。**推荐大家打开这个开关，新的版本通常会修复 bug 已经加入新的功能，让 PicGo 更好用 ~**

### 开机自启

选择是否开机自启动。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/autoStart.png)

### 上传前重命名

如果你想在图片上传前能够有机会改动你的图片名，那么可以选择开启图片上传前重命名：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/rename_before_upload.png)

之后你在上传的时候就会弹出一个小窗口让你重命名文件。如果你不想重命名，点击确定、取消或者直接关闭这个窗口都是可以的。如果你想要重命名就在输入框里输入想要更改的名字，然后点击确定即可。另外这个特性也支持批量上传，如下：

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/picgo_rename.gif)

### 选择想要显示的图床

很多时候你并不会使用上 PicGo 给你提供的全部的图床。所以为了精简显示你可以只选择你想要的图床来显示，这样侧边栏也就不会出现滚动条了。不过需要注意的是，这个仅仅是显示 / 隐藏而并不是剔除相应的功能。假如你隐藏了七牛云，你依然是可以通过七牛云来上传图片的。

![img](https://raw.githubusercontent.com/Molunerfinn/test/master/picgo/picbed-choose.gif)

### 上传提示

![img](https://camo.githubusercontent.com/763757f281c0a19ee526f26bbb1a2814f164879b/68747470733a2f2f692e6c6f6c692e6e65742f323031382f30362f30352f356231363832666134316337302e706e67)打开之后会在每次上传图片的时候弹出提示框提示正在上传

### 自动时间戳命名

![img](https://camo.githubusercontent.com/25e5d680bfd19a086611871ac4621c5b079a9c99/68747470733a2f2f692e6c6f6c692e6e65742f323031382f30362f30352f356231363833623334366236372e706e67)开启之后会自动将上传的文件名替换成时间戳：![]([https://user-images.githubusercontent.com/12621342/40976264-2de18afe-6900-11e8-8f35-746820632eb8.png）](https://user-images.githubusercontent.com/12621342/40976264-2de18afe-6900-11e8-8f35-746820632eb8.png%EF%BC%89)

### 检查更新

![img](https://user-images.githubusercontent.com/12621342/40976407-ad43d07c-6900-11e8-854f-15e1c41a7d8d.png)用以主动发起更新检查。