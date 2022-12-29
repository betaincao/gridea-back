---
title: 'prometheus相关case记录'
date: 2022-11-25 17:02:05
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
1、kube-system/kube-state-metrics指标数据太多，未分片导致拉取不到指标，通过分片、增加kube-system/kube-state-metrics副本数解决。