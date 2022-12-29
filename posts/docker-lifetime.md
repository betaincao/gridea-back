---
title: 'docker lifetime'
date: 2021-11-16 14:15:52
tags: [docker]
published: true
hideInList: false
feature: /post-images/docker-lifetime.png
isTop: false
---
直接上图：
![](https://betaincao.github.io//post-images/1637043469549.png)
解读：
1、容器状态（上图中带颜色的圆圈）：Created，Running，Paused，Stopped，Deleted；
2、Docker命令：docker run，docker create，docker stop，docker rm，docker pause，docker kill，docker unpause等；
3、docker相关事件（上图中的矩形框）：create，start，die，stop，OOM等；
4、重启策略判断条件：根据重启策略（restart policy）判断是否需要重启容器

## 第一条路径：
![](https://betaincao.github.io//post-images/1637043979518.png)
如上图所示:
1、我们先通过 docker run 命令，直接创建（ create ）并启动（ start ）一个容器，进入到运行状态（ Running ）
2、然后程序运行结束（例如输出 Hello World 之后，或者通过 Ctrl + C 使得程序终止），容器死亡（ die ）
3、由于我们没有设置重启策略，所以直接进入到停止状态（ Stopped ）
4、最后通过 docker rm 命令销毁容器，进入到被删除状态（ Deleted ）

## 第二条路径：
![](https://betaincao.github.io//post-images/1637044084057.png)
如上图所示：
1、我们还是通过 docker run 命令，直接创建（ create ）并启动（ start ）一个容器，进入到运行状态（ Running ）
2、然后通过 docker stop 命令杀死容器中的程序（ die ）并停止（ stop ）容器，最终进入到停止状态（ Stopped ）
3、最后通过 docker rm 命令销毁容器，进入到被删除状态（ Deleted ）

### tips:
docker stop与docker kill 区别：
kill 命令向容器内运行的程序直接发出 SIGKILL 信号（或其他指定信号），而 stop 则是先发出 SIGTERM 再发出 SIGKILL 信号，属于优雅关闭（ Graceful Shutdown ）。推荐使用docker stop。