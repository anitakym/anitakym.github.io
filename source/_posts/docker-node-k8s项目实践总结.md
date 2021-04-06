---
title: docker-node-k8s项目实践总结
date: 2021-04-03 12:21:24
tags:
---
### 推荐学习资料:
一定要点开，完整而全面 —— 也是frontend masters上面的一门课
https://btholt.github.io/complete-intro-to-containers/

### 上述资料概述
TABLE OF CONTENTS（目录）
- Welcome
  - Introduction
- Crafting Containers By Hand
  - What Are Containers? (什么是容器？)
  - chroot 
  - Namespaces (命名空间)
  - cgroups
- Docker
  - Getting Set Up with Docker (使用Docker进行设置)
  - Docker Images without Docker
  - Docker Images with Docker
  - Node.js on Docker
  - Tags (标签)
  - Docker CLI
- The Dockerfile
  - Intro to Dockerfiles (Dockerfiles介绍)
  - Build a Node.js App (构建一个Node.js应用)
  - A More Complicated Node.js App (一个更复杂的Node.js应用)
  - A Note on EXPOSE (关于EXPOSE的说明)
  - Layers
- Making Tiny Containers
  - Alpine Linux
  - Making Our Own Alpine Node.js Container (制作我们自己的Alpine Node.js容器)
  - Multi Stage Builds
  - Static Assets Project
- Features in Docker
  - Bind Mounts
  - Volumes
  - Using Containers for your Dev Environment (在开发环境中使用容器)
  - Dev Containers with Visual Studio Code
  - Networking with Docker
- Multi Container Projects (多容器项目)
  - Docker Compose
  - Kubernetes
  - Kompose
- OCI (Non-Docker) Containers （OCI(非Docker)容器）
  - Buildah
  - Podman
- Wrapping Up (收尾工作)
  - Conclusion (结论)

PS：把材料放到github,也是因为文本材料的错误不可能完全无一点错误，所以放到github上，大家都可以提issue（问题），这样后续的人，就能方便查到了；而材料也能在这个过程中不断得完善; video课程收费，但是材料开源;


### 项目介绍


### 存在问题



### 做的优化