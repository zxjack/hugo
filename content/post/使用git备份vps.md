---
title: "使用git备份vps"
subtitle:    ""
description: ""
date: 2018-07-27T17:34:50+08:00
author:      "Zhengx"
image:       ""
tags:        ["Tech", "Docker"]
categories:  ["Tech","Docker" ]
published: true
showtoc: false 
---



## 写在前面：

之前在购买的vps上搭建各种服务经常用的是网络上找到的一键脚本，尽管已经比较方便了，但是每次搞还是要折腾很久。包括环境的搭建，各种配置等。我又是比较喜欢折腾的，在尝试新的东西的时候不可避免要出现各种错误把系统搞的一塌糊涂。如果这个时候要重新重装系统RESET，那就麻烦了。如果能够方便的重置呢，我最近在学习Docker的过程中尝试使用Docker+Git能够比较方便的解决这个问题。

<!-- more -->

## 前期准备工作

1. git的准备，git的使用可能很方便的进行版本控制，同时通过`git pull`将需要备份的文件传输到备份服务器上， `git clone`将需要的文档从服务器端拉回来。
2. 对于git库的选择我最终选择了[gitlab](https://gitlab.com/),其中最主要的原因是gitlab支持私人库，而github是必须公开的，作为备份文件就不太方便了。
3. vps上目前大部分系统默认是按照好git的，反正我用的搬瓦工上debian 9是带的。如果没有git，就需要提前安装一下了。
4. gitlab上需要创建一个新的Projects，用于备份使用，如果没有账户就先注册一个吧。

## 正式开始

- 在新的vps上安装docker环境，可以参考这个教程：**[Debian 9 安装 docker ce](https://blog.csdn.net/hnhbdss/article/details/78512651)**
- 安装docker-compose，安装命令如下：

```
curl -L https://github.com/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > ~/docker-compose 
sudo  mv   ~/docker-compose     /usr/local/bin/
sudo chmod +x /usr/local/bin/docker-compose
```

- 使用docker-compose将需要的服务配置好
- 配置git环境使用以下命令：

```
git init
git remote add git@gitlab.com:user/mybackup.git #添加自己的project地址
git add .
git commit -m "my bakcup"
git push -u origin master
```

- 这样就完成了将本地的配置上传服务器。这里需要注意的是需要将备份的文件都放在同一个目录下，如果不在同一个目录下，文件是不会备份的。
- 恢复备份的时候就更加简单了一个命令搞定:

```
git clone git://gitlab.com/####/####.git #之前添加的project地址
```

- 拉回之间的配置之后在目录下运行

```
docker-compose up -d
```

在这种情况下，我可以愉快的玩耍了，一旦折腾出了问题可以随时从gitlab上将之前好的配置恢复到本地，一键恢复。





