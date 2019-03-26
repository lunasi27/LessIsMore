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
------------------------------------
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
------------------------------------
vi /etc/docker/daemon.json

添加

{

  "registry-mirrors": ["\<your accelerate address\>"]

}

运行命令:

systemctl daemon-reload

service docker restart


宿主机设置了proxy导致kubenetes添加node不成功的问题
------------------------------------
原因：

宿主机因为设置了proxy导致kubectl命令无法执行，取消代理可以执行kubectl。但是，docker无法连接internet，导致docker pull无法成功执行。

解决方案：

1,将本机IP加入到NO_PROXY列表中

export NO_PROXY=<host_ip>,$NO_PROXY

2,取消宿主机的proxy环境变量设置，而给docker添加PROXY

mkdir -p /etc/systemd/system/docker.service.d

vi /etc/systemd/system/docker.service.d/http-proxy.conf

    [Service]

    Environment="HTTP_PROXY=<proxy_address>:<port>/"

vi /etc/systemd/system/docker.service.d/https-proxy.conf

    [Service]

    Environment="HTTPS_PROXY=<proxy_address>:<port>/"

vi /etc/systemd/system/docker.service.d/-proxy.conf

    [Service]

    Environment="NO_PROXY=<proxy_address>,<proxy_address>"

systemctl daemon-reload

systemctl restart docker

systemctl show --property=Environment docker