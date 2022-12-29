---
title: 'docker常用命令'
date: 2022-07-11 14:48:15
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
docker ps 查看正在运行的docker容器，相当于操作系统查看进程命令；
docker ps -a 查看所有运行过的容器，包括已经停止运行的容器；
docker stop <container id> 停止某个正在运行的容器
docker start  <container id> 启动某个已经停止的容器
docker images 获取本地所有的容器镜像
docker run <image id> 运行某个镜像
docker logs -f <container id> 查看容器运行日志
docker exec -it <container id> /bin/bash 进入一个正在运行的镜像内
docker rm <container id> 删除某个未来运行状态的容器
docker rmi <image id> 删除某个镜像，只能删除未运行过的镜像
docker inspect <image id> 查看某个镜像的详细信息，包括层目录等等
