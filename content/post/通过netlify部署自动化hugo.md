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

作为非IT人事，完全靠google搞定了在netlify上自动化部署hugo，不得不佩服一下自己。这个文章作为部署的记录，重新复习一下过程。

### 第一步 在本地部署hugo  

hugo的安装非常简单，上hugo的官方网站：https://gohugo.io/可以查看相关的文档包括安装说明等。我是在windowns 10的环境中使用的，所以就下载[**hugo_0.44_Windows-64bit.zip**](https://github.com/gohugoio/hugo/releases/download/v0.44/hugo_0.44_Windows-64bit.zip)到本地，然后解压到一个目录下就好了。hugo的版本发布可以在下面的地址：https://github.com/gohugoio/hugo/releases进行查看。注意：

- 下载解压之后，hugo.exe命令只能在当前的文件夹中运行，这个比较麻烦，我是在系统中添加了变量PATH之后解决了这个问题。这样我就可以在任何地方执行hugo命令了。

hugo的环境搭建也是比较简单的，按照如下步骤进行：（Windows）

1. 建立需要运行的目录例如`hugo`

2. 进入相应的目录

   ``` bash
   cd hugo
   ```

3. 初始化hugo

   ```bash
   hugo new site mysite
   ```

4. 然后 hugo 会自动生成这样一个目录结构： 

   ```
    ▸ archetypes/
    ▸ content/
    ▸ layouts/
    ▸ static/
    config.toml
   ```

其中config.toml是配置文件，content中放的是markdown文章，static里面放的是网站用到的相关资料，如图片等。

5. **执行相应的命令需要在创建的网站目录mysite中运行**

   ```
   cd mysite
   ```

   

6. 建立博客文章

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

7. hugo有个坑，初始化之后默认是没有主题的，需要至少下载一个主题才能使用。我用的是hugo-theme-cleanwhite

     ```
git submodule add https://github.com/zhaohuabing/hugo-theme-cleanwhite themes/hugo-theme-cleanwhite
     ```

之所以用`git submodule`是为了之后在netlify中使用。

8. 在本地进行测试运行下面的命令

    ```
hugo serve -t  hugo-theme-cleanwhite
    ```

然后在本地通过访问http://127.0.0.1:1313进行测试



### 第二步 注册github帐号，并新建一个repo用于hugo使用

### 第三步 将本地调试好的hugo项目上传至github

### 第四步 注册netlify帐号，并设置相关内容



![mark](http://onqn9gsrl.bkt.clouddn.com/blog/180720/HgKk4dD4jl.png?imageslim)







