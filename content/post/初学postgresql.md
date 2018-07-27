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