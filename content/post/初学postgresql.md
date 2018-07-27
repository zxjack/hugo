---
title: "初学postgresql"
subtitle:    ""
description: ""
date: 2018-07-27T22:30:21+08:00
author:      "Zhengx"
image:       ""
tags:        ["Tech", "PostgreSQL"]
categories:  ["Tech" ]
published: true
showtoc: false 
---



刚刚接触PostgreSQL，完全是懵逼的状态，记录一下学习的过程。

进入 PostgreSQL 命令行

```
su - postgres #切换到 postgres 用户
```
![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224422.png)

```
psql
```

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224604.png)

列出数据库：

```
\l
```

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224656.png)

切换数据库：

```
\c dbname
```

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224801.png)

列出数据表 :

```
\d
```

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224840.png)

退出：

```sql
\q
```
![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727224951.png)

Did not find any relation named：名字加引号。

数据库的备份：

在运行数据库的docker中用postgres用户运行一下命令

```
pg_dump 数据库名称 > 备份文件.dump
```

![](https://pic-1253455688.cos.ap-shanghai.myqcloud.com/20180727232757.png)

数据库的恢复

恢复 pg_dump 出来的文件使用命令：

```
 psql 数据库名称 < 备份文件.dump
```
