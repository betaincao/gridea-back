---
title: '编写自定义的kubernetes controller'
date: 2021-11-08 16:09:16
tags: [kubernetes,golang]
published: true
hideInList: false
feature: /post-images/bian-xie-zi-ding-yi-de-kubernetes-controller.jpeg
isTop: false
---
当我们需要监控某个资源的变化并做一些列的操作时，使用k8s提供的controller机制来实现，k8s官方提供了提个通用库client-go。
![](https://betaincao.github.io//post-images/1636359463968.jpeg)
如上图所示，图中包含了client-go与controller的整个交互过程。



