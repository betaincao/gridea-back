---
title: 'golang - channel'
date: 2021-08-25 12:03:25
tags: [golang]
published: true
hideInList: false
feature: 
isTop: false
---
go语言中最常见的、也是经常被人提及的设计模式--不要使用共享内存的方式通信，应该通过通信的方式共享内存。
## channel的特性
1、先入先出（FIFO）
2、无锁管道

## 关闭channel的方式
1、context
2、done channel

## 有缓存&无缓存管道
无缓存channel实际上可以看做是一种同步模式，有缓存的channel可以看做是异步模式。
在同步模式下，发送方和接收方要同步就绪，只有两者都ready的情况下，数据才能在两者间传递（实际是内存拷贝）。
在异步模式下，在缓冲区可用的情况下（有剩余容量），发送方和接收方都可以顺序运行。
同步模式下，必须要发送方和接收方配对，操作才能成功，否则会被阻塞；异步模式下，缓冲槽要有剩余容量，操作才能成功，否则也会阻塞。

注：函数间传递chan时，直接传递channel，不用传递channel的指针。

## channel的底层实现原理
我们先看一个简单地小demo：
```sh

 package main

 func main() {
     ch := make(chan struct{})
     ch <- struct{}{}
 }
```
创建了一个无缓冲channel，然后往这个channel发送数据。因为程序中没有读操作ready，所以发送的时候会阻塞。
