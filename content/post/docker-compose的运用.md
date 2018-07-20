---
title: docker compose的运用
date: 2018-07-18 16:57:27
categories:  ["Tech"]
showtoc: false 
tags: 
- docker
typora-root-url: ..\..\static
---
从去年开始，在qnap上开始学习使用docker。发现docker真是个好东西，可以在linux上不断的随便折腾，搞错了就删掉然后重新来过，非常适合新手。另外，也非常适合在不同vps上进行部署，完全不用管底层系统是啥，debian，Ubuntu都可以。而且，现在在<https://hub.docker.com>上有很多封装好的docker images，可以直接pull下来，直接运行使用。  
<!--more-->

## 初识docker compose  

最开始使用docker都是用的`docker run `来运行docker，但是在后期随着docker运行的越来越多就涉及到多个docker之间的协调。在这种情况下，经常需要协调多个docker，在调试过程中要同时调整多个docker的设置，多次重启docker。尤其是在设计到nginx、v2ray、aria2c、nextcloud等，直接用`docker run `来搞好麻烦的。在看到docker-compose之后发现这个是神器呀，必须学习使用。  

### docker compose 是什么？  

Docker-Compose 是 Docker 的一种编排服务，是一个用于在 Docker 上定义并运行复杂应用的工具，可以让用户在集群中部署分布式应用。通过 Docker-Compose 用户可以很容易地用一个配置文件定义一个多容器的应用，然后使用一条指令安装这个应用的所有依赖，完成构建。Docker-Compose 解决了容器与容器之间如何管理编排的问题，大概的工作原理为：

![docker-compose](/img/docker-compose.png)

用通俗的话来说，docker compose就是一个批处理，可以将多个docker通过一个批处理进行统一的调度是使用。  

## docker compose的常用命令

`docker-compose up` 启动docker，这个命令是将docker运行在前台，适用于在调试阶段，可以通过screen看到运行的情况，如果有错误，用ctrl+c进行停止。  

`docker-compose up -d` 将docker在后台运行

`docker-compose down` 停止docker 

需要注意的是通过docker-compose运行docker，在每一次运行和停止的时候，都会进行初始化设置，也就是启动的时候创建相关的网络、容器，停止的时候就会删除相关的容器同时移除相关网络。  

## docker compose最重要的配置文件  

docker compose的运行是完全依赖于文件docker-compose.yml，这个文件就是docker compose的核心。通过创建、修改这个文件达到配置多个docker的目的。  

```yml
version: '2'

services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro

  whoami:
    image: jwilder/whoami
    environment:
      - VIRTUAL_HOST=whoami.local
```

上面就是一个例子，通过docker-compose.yml设置了nginx-proxy，具体使用请google。
