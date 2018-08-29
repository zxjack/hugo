---
title: "打通内外网最后一公里：nginx配置"
subtitle:    ""
description: ""
date: 2018-08-29T11:36:48+08:00
author:      "Zhengx"
image:       ""
tags:        ["Tech", "Net"]
categories:  ["Tech" ]
published: true
showtoc: false 
---

## 写在前面

之前已经完成了服务器端和路由器端的frp部署，接下来就是要将不同的域名服务分配到实际提供服务的后端服务器上，nginx的反代功能能够很好的解决这个需求，而且配置起来也不是太麻烦。同时除了可以提供http域名访问之外，还可以配置https访问，基本上完美的解决我的需求了。

> 例如：在局域网内通过http://192.168.0.30:8123 访问homeassiant服务，配置完成后可以通过https://hass.myhome.net 进行访问。

### 前期准备工作

1. 注册一个域名
2. 将需要的域名在DNS服务商那边解析到公网上的服务器IP地址

### 开始部署nginx

目前大部分的linxu系统都可以比较方便的安装nginx，debian中可以通过以下的命令进行安装

```
sudo apt-get update
sudo apt-get install nginx
```

nginx的主要启动，重启，状态查询命令

```
sudo service nginx stop         #停止
sudo service nginx start        #启动
sudo service nginx restart      #重启
sudo update-rc.d nginx defaults #系统重启之后自动重启nginx服务
sudo nginx -t                   #测试配置是否正确
sudo nginx -s reload			#重新载入配置文件，一般在修改了配置之后需要运行以便新的配置生效
```



安装完成之后对nginx进行配置，主要的配置文件目录为：

```
/etc/nginx/ #nginx的配置文件目录
/etc/nginx/sites-enabled/ #域名对应的配置文件目录
```

- nginx.conf是全局配置文件，为了更好的管理不建议在这个文件设置具体的域名服务
- 具体的域名代理服务建议在/etc/nginx/sites-enabled/目录下建对于的文件来进行专门的配置。
- 例如需要对域名**wifi.home.net**这个域名进行进行代理，则在目录下建一个文件名为`wifi.home.net`的文件，在文件中进行配置。
- **wifi.home.net**文件：

```
server {
        listen 80;
        server_name wifi.home.net;  #具体的域名
        proxy_pass         http://192.168.0.10:8888;  #局域网内提供服务的ip地址以及端口
        # proxy_redirect     off;
        # proxy_set_header   Host             $host;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection “upgrade”;  
 }
```

上述配置文件适用于大部分服务的反代理，需要修改的地方是`server_name` 修改为需要代理的域名和`proxy_pass` 实际提供服务的ip地址和服务。设置完成之后，必须运行`nginx -s reload` 重新载入配置文件才会生效。

完成上述设置之后，可以在浏览器中输入http://wifi.home.net 进行访问，而且不限于局域网中，在外网也是能够直接访问的。

