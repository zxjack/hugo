---
title: "Hugo Test"
subtitle:    ""
description: ""
date: 2018-07-19T22:29:54+08:00
author:      ""
image:       ""
tags:        ["测试", "hugo","Tech"]
categories:  ["Tech"]
showtoc: false 

typora-copy-images-to: ..\..\static\img
typora-root-url: ..\..\static
---


写在前面，为啥用hugo，最主要的原因是之前尝试了hexo，挺好用的。但是考虑到一旦电脑更换了，就需要重新部署。另外也尝试了自动化部署hexo，但是在gitlab上用CI自动部署好慢呀。最终选了hugo，从目前使用的情况来看，还是明显比hexo快不少。但是就部署而言还是比较麻烦的。

1.测试一下推送是否能够成功 ：成功

2.使用Typora,插入图片进行测试。自动插入、保存到相应的目录，试试看。

![36543aa043111845f4d1ff236c383664](/img/36543aa043111845f4d1ff236c383664.jpg)

成功。注意在Typora中要设置对图片的默认位置，将设置图片根目录设置到hugo工作目录下的static就可以了，千万不要设置到img目录中，这样在拖拽图片进行插入的时候才能设置正确的图片相对目录。为了更加方便的使用，实现在本地拖拽图片自动复制到相应的目录，在文档中选用对的相对路径设置以确保文档图片正确显示， 建议采取如下步骤：

- 设置**编辑-图片工具-设置图片根目录**（将目录设置到hugo工作目录/static）
- 设置**编辑-图片工具-插入本地图片时-复制到文件夹**（将目录设置到hugo工作目录/static/img）

3.每次写好文章更新的时候都要重复输入命令，太烦了。参考网上的帖子，改了一下，写了个脚本，一个命令搞定。新建个deplay.sh将脚本复制并保存在hugo根目录下。需要更新的时候输入`./deploy.sh`就ok了。

```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

git add .
# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master



```

