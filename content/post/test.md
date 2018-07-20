---
title: "Test"
subtitle:    ""
description: ""
date: 2018-07-19T22:29:54+08:00
author:      ""
image:       ""
tags:        ["测试", "hugo"]
categories:  ["TECH"]
showtoc: false 

typora-copy-images-to: ..\..\static\img
typora-root-url: ..\..\static
---
1.测试一下推送是否能够成功 ：成功

2.使用Typora,插入图片进行测试。自动插入、保存到相应的目录，试试看。

![36543aa043111845f4d1ff236c383664](/img/36543aa043111845f4d1ff236c383664.jpg)

成功。注意在Typora中要设置对图片的默认位置，将设置图片根目录设置到hugo工作目录下的static就可以了，千万不要设置到img目录中，这样在拖拽图片进行插入的时候才能设置正确的图片相对目录。为了更加方便的使用，实现在本地拖拽图片自动复制到相应的目录，在文档中选用对的相对路径设置以确保文档图片正确显示，建议采取如下步骤：

- 设置**编辑-图片工具-设置图片根目录**（将目录设置到hugo工作目录/static）
- 设置**编辑-图片工具-插入本地图片时-复制到文件夹**（将目录设置到hugo工作目录/static/img）

