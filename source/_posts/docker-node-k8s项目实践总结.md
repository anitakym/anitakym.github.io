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

### 存在问题



### 做的优化



### 随便聊聊
之前看了阿里巴巴云原生的一篇访谈博文（https://juejin.cn/post/6951283312824418311）：
里面Nacos联合创始人做了一个类比：Nacos之于微服务的地位，就跟Etcd之于k8s的地位一样


翻译内容笔记来自于下面开源链接：
https://btholt.github.io/complete-intro-to-containers/




