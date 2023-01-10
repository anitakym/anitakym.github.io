---
title: 第一本docker书-精读
date: 2021-05-24 20:25:44
tags:
---

## docker hub 镜像加速
- https://y0ngb1n.github.io/a/docker-registry-mirrors.html?js

### history

- 容器技术 - Linux的进程模型对于容器本身的重要意义； “控制器”模型对Kubernetes的作用
- PasS - 提供了一套应用打包的功能 - 帮助用户大规模部署应用到集群里 - 但是也是一个问题
- Docker 对 PasS，降维打击 -> 因为提供了非常方便的打包机制，直接打包了系统，保证了本地和云端环境的一致，减少“试错”成本
- Fig 项目 - container orchestration - 容器编排
- OCI -  将容器运行时和镜像的实现从Docker项目中剥离出来
- CoreOS - Etcd
- Docker公司 - 将开源项目和商业产品绑定 - 技术生态的封闭
- Kubernetes - 开发者为核心 - 民主开放的容器生态