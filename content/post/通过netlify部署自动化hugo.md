---
title: "通过netlify部署自动化hugo"
subtitle:    ""
description: ""
date: 2018-07-20T16:13:19+08:00
author:      "Zhengx"
image:       ""
tags:        ["hugo", "netlify"]
categories:  ["Tech" ]
published: true
showtoc: false 
---



##  小白如何搞定自动化部署hugo呢？

作为非IT人事，完全靠google搞定了在netlify上自动化部署hugo，不得不佩服一下自己。这个文章作为部署的记录，重新复习一下过程。一共分四步，慢慢往下看吧。

#### 写在前面：

*为啥要搞的这么复杂呢，最主要的原因是我比较懒，就想着前期搞定了之后，后期只要有一台电脑能够git推送博客到github上就不用管其他的事情了，netlify能够自动的帮我生成相应的页面，同时，万一哪一天写博客的电脑坏了也不需要重新部署，仅仅需要将github上的项目`git clone`下来然后就可以更新了。前期麻烦一些，后面省事了。*

#### 第一步 在本地部署hugo  

hugo的安装非常简单，上hugo的官方网站：https://gohugo.io/可以查看相关的文档包括安装说明等。我是在windowns 10的环境中使用的，所以就下载[**hugo_0.44_Windows-64bit.zip**](https://github.com/gohugoio/hugo/releases/download/v0.44/hugo_0.44_Windows-64bit.zip)到本地，然后解压到一个目录下就好了。hugo的版本发布可以在下面的地址：https://github.com/gohugoio/hugo/releases进行查看。注意：

- 下载解压之后，hugo.exe命令只能在当前的文件夹中运行，这个比较麻烦，我是在系统中添加了变量PATH之后解决了这个问题。这样我就可以在任何地方执行hugo命令了。

hugo的环境搭建也是比较简单的，按照如下步骤进行：（Windows）

1.建立需要运行的目录例如`hugo`  

2.进入相应的目录  

   ``` bash
   cd hugo
   ```

3.初始化hugo

   ```bash
   hugo new site mysite
   ```

4.然后 hugo 会自动生成这样一个目录结构： 

   ```

    ▸ archetypes/
    ▸ content/
    ▸ layouts/
    ▸ static/
    config.toml
   ```

其中config.toml是配置文件，content中放的是markdown文章，static里面放的是网站用到的相关资料，如图片等。

5.**执行相应的命令需要在创建的网站目录mysite中运行**

   ```
   cd mysite
   ```

6.建立博客文章

```
hugo new post/myblog.md #建立博客日志，创建的博客日志在content/post目录中
```

可以用markdown编辑软件进行编辑了，推荐使用Typora。这里有一个需要注意的地方，由于我不在本地生成静态页面，所以需要将默认建立的模版进行修改。最主要的是把`draft = true `去掉。我修改之后的模版如下（默认的模版是/archetypes/default.md这个文件）：

```yaml

---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
subtitle:    ""
description: ""
author:      ""
image:       ""
tags:        ["tag1", "tag2"]
categories:  ["TECH"]
showtoc: false

---

```

7.hugo有个坑，初始化之后默认是没有主题的，需要至少下载一个主题才能使用。我用的是hugo-theme-cleanwhite

```
git submodule add https://github.com/zhaohuabing/hugo-theme-cleanwhite themes/hugo-theme-cleanwhite
```

之所以用`git submodule`是为了之后在netlify中使用。

8.在本地进行测试运行下面的命令

```
hugo serve -t  hugo-theme-cleanwhite –-watch
```

然后在本地通过访问http://127.0.0.1:1313进行测试

部署完成之后类似这样的页面：

![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/7l190Lhiei.png?imageslim)

具体的操作建议大家Google吧，当然查看官方文档也是挺好的。

官方文档：<https://gohugo.io/overview/introduction/> 

皮肤列表：<https://github.com/spf13/hugoThemes> 

常用文档：

1. [Configuring Hugo](https://gohugo.io/overview/configuration/)

2. [Front Matter](https://gohugo.io/content/front-matter/)

3. [Menus](https://gohugo.io/extras/menus/)

4. [Template Variables](https://gohugo.io/templates/variables/)

5. [Hosting on GitHub Pages](https://gohugo.io/tutorials/github-pages-blog/)

   

#### 第二步 注册github帐号，并新建一个repo用于hugo使用  



这个一步很简单，首先是登录github的网站：https://github.com

如果没有用户，先进行相关注册，注册之后登录页面，选择创建项目（Start a project）

![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/f9J6GcJJAd.png?imageslim)

在Repository name中写入想要的名字，例如hugo，然后点击Create repository就完成项目的创建了。新创建的项目是一个空的，这个时候需要记录下项目的地址

![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/IH9DAjILCC.png?imageslim)

就是像`git@github.com:user/test.git`这样的地址，后面有用。页面中列举了git的基本命令，我也就学会了这几个就够用了。

```git
echo "# test" >> README.md #创建一个README.md文件并将test写入其中
git init  #初始化
git add README.md  #添加文件用于上传
git commit -m "first commit" #准备上传并写入上传的原因
git remote add origin git@github.com:user/test.git #添加上传的项目以及地址
git push -u origin master #上传文件
```

备注：

*在Windows中没有git的命令，需要从github网站下载安装。*

*github下载地址：https://git-scm.com/downloads*

git相关介绍，还是Google吧，网上有很多。

#### 第三步 将本地调试好的hugo项目上传至github

当我们将hugo在本地调试完成之后，将项目推送到github上，命令如下

```git
git add .
git commit -m "hugo blog"
git remote add origin git@github.com:user/test.git
git push -u origin master
```

上传完成之后可以登录到github上进行查看，后期更新博客也是用上面的命令，只不过不需要第三的命令了。到此已经完成了前期的准备工作，就剩下最后一步就可以搞定自动化部署hugo了。

#### 第四步 注册netlify帐号，并设置相关内容

我是通过Google找到了这篇文字（[Hugo 网站托管至 Netlify](https://www.choyang.me/zh/post/hosting-hugo-on-netlify/)）发现了这个奥义。Netlify 支持编译 Github 仓库的代码，这样我们可以把 Hugo 网站源代码上传至 Github 用 Git 管理，然后在 Netlify 上发布网站。具体操作我是根据hugo网站上提供的介绍进行操作的。 英文好的可以自行查看：https://gohugo.io/hosting-and-deployment/hosting-on-netlify/

首先还是登陆netlify网站使用github帐号进行登陆。官方网站：https://www.netlify.com/

![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/HgKk4dD4jl.png?imageslim)

接下来会跳到github的授权页面进行授权。

![](https://d33wubrfki0l68.cloudfront.net/66276caf9e5deee836ba60fab50f78f6074e3ca0/0cc43/images/hosting-and-deployment/hosting-on-netlify/netlify-first-authorize.jpg)

从github中创建新的站点

![](https://d33wubrfki0l68.cloudfront.net/1a92de85be074abc024967fa7088c8b719c32466/f7496/images/hosting-and-deployment/hosting-on-netlify/netlify-add-new-site.jpg)

netlify会一步一步的带领我们完成建站的步骤，在接下里的页面中选择github

![](https://d33wubrfki0l68.cloudfront.net/742c7be22b24a5df82a39f7cd259a04a7abdd150/db696/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-1.jpg)

这个时候会再次出现github的授权页面，继续同意授权。

![](https://d33wubrfki0l68.cloudfront.net/dd85bd12e419baeb7ef56e45c43235d2004ce341/77531/images/hosting-and-deployment/hosting-on-netlify/netlify-authorize-added-permissions.jpg)

完成授权之后，在下一步选择用来建站的repository

![](https://d33wubrfki0l68.cloudfront.net/188f9bfa9eb4997757414ec0ac1979d7111c9741/8f7a6/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-2.jpg)

完成选择之后，就可以进行基本的设置了。我选择的是默认的`public`和`master`。

我是通过配置文件netlify.toml 设置hugo的版本，从网站上拷贝文件，然后将其推送至github上，netlify会自动根据配置文件进行部署。这一部分很容易一模一样复制粘贴就ok了。

netlify.toml ：

```yaml
[build]
publish = "public"
command = "hugo"

[context.production.environment]
HUGO_VERSION = "0.44"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"

[context.split1]
command = "hugo --enableGitInfo"

[context.split1.environment]
HUGO_VERSION = "0.44"
HUGO_ENV = "production"

[context.deploy-preview]
command = "hugo --buildFuture -b $DEPLOY_PRIME_URL"

[context.deploy-preview.environment]
HUGO_VERSION = "0.44"

[context.branch-deploy]
command = "hugo -b $DEPLOY_PRIME_URL"

[context.branch-deploy.environment]
HUGO_VERSION = "0.44"

[context.next.environment]
HUGO_ENABLEGITINFO = "true"

```

到此就完成了所有的步骤，点击“Deploy site” 就搞定了。netlify会立刻进行自动部署，同时在我们写完博客之后只要推送到github上，netlify就会自动的更新页面，等一下下我们刷新网站就可以看到发布的页面了。

![](https://d33wubrfki0l68.cloudfront.net/a9f55d92792a554cb775cd0d10eddf445338b83a/0a424/images/hosting-and-deployment/hosting-on-netlify/netlify-deploying-site.gif)

netlify发布hugo还是很快的，大概20秒左右就搞定了。

![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/eIB3L50777.png?imageslim)

