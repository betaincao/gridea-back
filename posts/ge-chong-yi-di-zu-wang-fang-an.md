---
title: '各种异地组网方案'
date: 2022-09-26 10:34:44
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
这些年内网穿透/异地组网的方案比较多
 
1. headscale(tailscale服务端开源版，基于wireguard ) 。教程近期多起来了，趋势热度比zerotier的越来越高，B站有教程，可以试试。（没用过，但最推荐）
相关链接：
https://icloudnative.io/posts/how-to-set-up-or-migrate-headscale/
 
https://github.com/gurucomputing/headscale-ui
 
https://b23.tv/LVBGssI
 
2. zerotier自建planet，（前面说没速度的怀疑用的是官方服务器打洞不成功流量被中转了）。
 
自建比较折腾，服务端需要修改源码，编译，每个客户端复制planet文件，和服务端部署前端UI部分。我目前采用这种方式，因为一直用zerotier，不想换其他工具。
 
优势：控制权限和路由配置简单，在UI层配置即可。
 
https://bit.ly/3SyIDF0
 
https://www.v2ex.com/t/869846
 
3. n2n，版本太多有点捋不清，跨版本打洞听说有问题，用好我觉得n2n才是最简单的，supernode和edge启动起来就几个参数
 
https://bit.ly/3RbhIy4
 
4. nebula 站长曾推荐过的
https://github.com/slackhq/nebula
 
https://www.v2ex.com/t/621442
 
配置需要深入阅读才知道怎么配置路由
 
5. 穿透/端口映射转发
 
frp/zoro/cloudflare tunnel
 
https://github.com/fatedier/frp
 
https://github.com/txthinking/zoro/blob/master/README_ZH.md
 
https://lxnchan.cn/cf-tunnel.html
 
https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/