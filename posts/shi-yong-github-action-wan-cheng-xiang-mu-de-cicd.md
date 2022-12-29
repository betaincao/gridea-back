---
title: '使用github action完成项目的CI/CD'
date: 2022-05-10 11:35:44
tags: [cicd]
published: true
hideInList: false
feature: 
isTop: false
---
记得之前dockerhub的自动构建功能是免费的，收费之后github的项目就不能再免费自动构建docker镜像并推送到dockerhub仓库了。
现在可以使用github action持续集成服务自动构建发布镜像到dockerhub，这里记录一下怎么使用github action去做自动构建推送镜像。
#### 配置github action的workflow
首先项目目录中需要有编写好的dockerfile，然后给项目新建.github/workflows/build-docker-image.yml文件，
```sh
# build-docker-image.yml
name: Publish Docker image   # workflow名称，可以在Github项目主页的【Actions】中看到所有的workflow

on:   # 配置触发workflow的事件
  push:
    branches:   # master分支有push时触发此workflow
      - 'master'
    tags:       # tag更新时触发此workflow
      - '*'

jobs:  # workflow中的job

  push_to_registry:  # job的名字
    name: Push Docker image to Docker Hub
    runs-on: ubuntu-latest   # job运行的基础环境

    steps:  # 一个job由一个或多个step组成
      - name: Check out the repo
        uses: actions/checkout@v2   # 官方的action，获取代码

      - name: Log in to Docker Hub
        uses: docker/login-action@v1  # 三方的action操作， 执行docker login
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}  # 配置dockerhub的认证，在Github项目主页 【Settings】 -> 【Secrets】 添加对应变量
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@v3  # 抽取项目信息，主要是镜像的tag
        with:
          images: betaincao/test-nginx # dockerhub中对应的镜像目录

      - name: Build and push Docker image
        uses: docker/build-push-action@v2 # docker build & push
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
```
配置中大部分都加上了注释，需要特别说明的是 steps 中的 uses 。 我们以第二个step Log in to Docker Hub 为例，正常情况下，我们应该是运行 run docker login ** 。 这里使用了一个 action docker/login-action，action 其实就是一系列step的组成，所以既然别人已经做好了，干嘛不直接用呢。所有可用的 action可以到 这里 查找。
#### 推送使用
配置妥当之后，提交代码推送至github。按照本例中的配置，只要master分支有push事件或者tag有更新，就会触发Github Action，然后自动构建镜像推送至DockerHub。
可以在Github项目主页的【Actions】栏中查看每次执行详情。