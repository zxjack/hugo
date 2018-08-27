---
title: "通过acme.sh自动部署UniFi Controller ssl证书"
subtitle:    ""
description: "使用**UniFi Controller** 默认是通过https://IP:8443 进行登录的，但是在这种情况下由于没有证书导致chrome在进行访问的时候总是会有警告。如何部署ssl证书是作为强迫症的人必须解决的问题。对于这个问题有很多的解决办法，免费而方便的就是通过acme.sh自动部署Let’s Encrypt 证书。这里提出的解决方案能够自动的申请证书并完成证书的导入。"
date: 2018-08-27T21:10:36+08:00
author:      "Zhengx"
image:       ""
tags:        ["unifi", "acme"]
categories:  ["Tech" ]
published: true
showtoc: false 
---



## 写在前面：

使用**UniFi Controller** 默认是通过https://IP:8443 进行登录的，但是在这种情况下由于没有证书导致chrome在进行访问的时候总是会有警告。如何部署ssl证书是作为强迫症的人必须解决的问题。对于这个问题有很多的解决办法，免费而方便的就是通过acme.sh自动部署Let’s Encrypt 证书。这里提出的解决方案能够自动的申请证书并完成证书的导入。

**LET'S GO**

---

### 前期的准备工作

- 安装acme.sh

```
curl https://get.acme.sh | sh
```

很方便，就一行命令就可以完成下载和安装，同时还能够安装一个自动化命令。由于Let’s Encrypt 申请的证书尽管是免费的，但是最长只有90天的有效期，这个命令将会在证书到期前自动的进行再次申请。完成安装之后最好重新连接一下ssh终端。如果需要可以通过命令获得证书更新的邮件提醒。

```
acme.sh --upgrade --auto-upgrade --accountemail "mynotifaction@email.com"
```

- 拥有一个自己的域名，acme.sh支持大部分的域名服务商，可以在这里进行 [DNS providers](https://github.com/Neilpang/acme.sh/tree/master/dnsapi) 具体的查询。  

###  创建一个post-hook file用于自动的备份原有证书和部署新的证书

创建这个文件`/root/.acme.sh/cloudkey-renew-hook.sh`，**以下代码完全不用做任何修改**

```bash
#!/bin/bash
# Renew-hook for ACME / Let's encrypt
echo "** Configuring new Let's Encrypt certs"
cd /etc/ssl/private
rm -f /etc/ssl/private/cert.tar /etc/ssl/private/unifi.keystore.jks /etc/ssl/private/ssl-cert-snakeoil.key /etc/ssl/private/fullchain.pem

openssl pkcs12 -export -in /etc/ssl/private/cloudkey.crt -inkey /etc/ssl/private/cloudkey.key -out /etc/ssl/private/cloudkey.p12 -name unifi -password pass:aircontrolenterprise

keytool -importkeystore -deststorepass aircontrolenterprise -destkeypass aircontrolenterprise -destkeystore /usr/lib/unifi/data/keystore -srckeystore /etc/ssl/private/cloudkey.p12 -srcstoretype PKCS12 -srcstorepass aircontrolenterprise -alias unifi

rm -f /etc/ssl/private/cloudkey.p12
tar -cvf cert.tar *
chown root:ssl-cert /etc/ssl/private/*
chmod 640 /etc/ssl/private/*

echo "** Testing Nginx and restarting"
/usr/sbin/nginx -t
/etc/init.d/nginx restart ; /etc/init.d/unifi restart
```

### 在DNS服务商那边获得证书申请所需要的DNS API

具体怎么申请请查看DNS官方网站，acme.sh支持多个DNS服务商的API完成证书申请工作，不同的服务商申请证书的方式不同。我用的是namesilo，这一部分的命令仅针对namesilo，将申请得到API KEY通过下面的命令进行输入。

```
export Namesilo_Key="YOUR-NAMESILO-API-KEY"
```

### 正式申请证书并完成部署

通过下面的命令进行证书申请，需要修改`unifi.myname.com`这个地方，将其修改为需要使用的域名。acme.sh命令在申请域名的证书的时候将域名增加在**-d**这个参数后面。

```
acme.sh --force --issue --dns dns_namesilo --dnssleep 900 -d unifi.myname.com --pre-hook "touch /etc/ssl/private/cert.tar; tar -zcvf /root/.acme.sh/CloudKeySSL_`date +%Y-%m-%d_%H.%M.%S`.tgz /etc/ssl/private/*" --fullchainpath /etc/ssl/private/cloudkey.crt --keypath /etc/ssl/private/cloudkey.key --reloadcmd "sh /root/.acme.sh/cloudkey-renew-hook.sh"
```

上面的命令除了完成证书申请之外，还将备份原有的证书，部署证书到unifi-control中，同时重启unifi服务。



