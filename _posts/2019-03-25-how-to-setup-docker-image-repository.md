---
layout: post
title:  如何修改docker的repository源
date:   2019-03-25 00:00:00 +0800
categories: 技术文章
tag: technology
---

* content
{:toc}


Docker 国内仓库和镜像			{#say-goodbyte}
====================================
由于众所周知的原因，我们在国内pull dockers image的时候，从官方Docker-Hub上下载会很慢。
所以，这里总结了一些国内能用的国内镜像。

Docker repository:

(china)

https://registry.docker-cn.com

http://hub-mirror.c.163.com

https://3laho3y3.mirror.aliyuncs.com

http://f1361db2.m.daocloud.io

https://mirror.ccs.tencentyun.com


(global)

https://hub.docker.com

https://quay.io

Docker 设置镜像源的方法
====================================
vi /etc/docker/daemon.json

添加

{

  "registry-mirrors": ["\<your accelerate address\>"]

}

运行命令:

systemctl daemon-reload

service docker restart