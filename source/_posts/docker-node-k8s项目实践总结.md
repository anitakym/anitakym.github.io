---
title: docker-node-k8s项目实践总结
date: 2021-04-03 12:21:24
tags:
---


### 项目介绍
```
#FROM xxx.xxx.xxx.cn/pub/nodejs:12.2.0_new
FROM xxx.xxx.xxx.cn/pub/nodejs:12.2.0_update
ARG VERSION
WORKDIR /xxx/xxx_target
COPY $VERSION/xxx_target.zip /xxxx/xxx_target

RUN  yum -y install  unzip ;  unzip xxx_target.zip ; /usr/bin/cp -r ./dependency/* /usr/share/fonts/ ; rm -f xxx_target.zip.zip 
ENTRYPOINT pm2 start ecosystem.config.js --env production --no-daemon
```
- unzip xxx_target.zip生成的流水线是：拉取gitlab代码，git pull && npm i && npm run ts:build
- 私有仓库是容器化部门构建的私有化仓库，基于harbor（https://github.com/goharbor）
- 日志落到集团kibana上面(https://github.com/elastic/kibana)
- 容器的性能和情况监控是在集团的grafana上面（https://github.com/grafana/grafana）
- mq,rabbitmq - 上部署的web管理端可以查看情况
- 最开始消费者是虚拟机和pod都有，我们根据ip段区分
- https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md
### 存在问题



### 做的优化



### 随便聊聊
之前看了阿里巴巴云原生的一篇访谈博文（https://juejin.cn/post/6951283312824418311）：
里面Nacos联合创始人做了一个类比：Nacos之于微服务的地位，就跟Etcd之于k8s的地位一样


翻译内容笔记来自于下面开源链接：
https://btholt.github.io/complete-intro-to-containers/


## Others
### harbor
#### projects
- 项目 ｜ 镜像仓库
- docker pull xxx.xxx.xxx.cn/project-x/xxxserver:202107071844
- 运维对我们项目的包优化了一个版本，增加了镜像大小 700M->1.12G，减少了下载的时间
#### API 控制中心 devcenter
