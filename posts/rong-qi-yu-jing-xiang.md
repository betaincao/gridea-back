---
title: '容器与镜像'
date: 2021-08-25 14:12:08
tags: [docker]
published: true
hideInList: false
feature: 
isTop: false
---
##  什么是容器？
容器是一个**视图隔离**、**资源可限制**、**独立文件系统**的进程集合。
###  视图隔离
所谓“视图隔离”就是能够看到部分进程以及具有独立的主机名等；因为进程之间相互可见并且可以相互通信，使用Namespace技术来实现进程在资源上的视图隔离。
### 资源可限制
控制资源使用率是可以对于内存大小以及CPU使用个数等进行限制；通过Cgroup来限制资源使用率，设置能够使用的CPU和内存量。
### 独立文件系统
针对不同进程使用同一个文件系统所造成的问题而言，Linux 和 Unix 操作系统可以通过 chroot 系统调用将子目录变成根目录，达到视图级别的隔离；进程在 chroot 的帮助下可以具有独立的文件系统，对于这样的文件系统进行增删改查不会影响到其他进程。

## 什么是镜像？
运行容器所需要的所有文件集合——容器镜像
Dockerfile - 描述镜像构建步骤

构建步骤所产生出文件系统的变化 - changeset
changeset的**分层**和**复用**
### changeset的分层和复用优势
1、提高分发效率
2、下载镜像时只需要下载本地没有的数据即可
3、节约系统资源

## 容器运行时的生命周期
### 单进程模型
1、Init进程生命周期 = 容器生命周期
2、运行期间可运行exec执行运维操作
### 数据持久化
1、独立于容器的生命周期
2、数据卷 - docker volume vs bind

## 容器项目架构
moby是目前最流行的容器管理引擎，moby daemon会对上提供关于容器、镜像、网络以及volume的管理。
### moby 容器引擎架构
moby daemon锁依赖的最重要的组件是containerd，containerd 是一个容器运行时管理引擎，其独立于 moby daemon ，可以对上提供容器、镜像的相关管理。
containerd 底层有 containerd shim 模块，其类似于一个守护进程。
![](https://betaincao.github.io//post-images/1629874274977.jpg)
containerd
容器运行时

## 容器 VS VM
容器是