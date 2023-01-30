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


## baiscs
#### cluster ip
- https://kubernetes.io/docs/concepts/services-networking/service/
```
Kubernetes assigns this Service an IP address (sometimes called the "cluster IP"), which is used by the Service proxies (see Virtual IPs and service proxies below).
```
- https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies
> ClusterIP: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default ServiceType.
```
举个例子，考虑一个图片处理后端，它运行了 3 个副本。这些副本是可互换的 —— 前端不需要关心它们调用了哪个后端副本。 然而组成这一组后端程序的 Pod 实际上可能会发生变化， 前端客户端不应该也没必要知道，而且也不需要跟踪这一组后端的状态。

Service 定义的抽象能够解耦这种关联。

Kubernetes 为该服务分配一个 IP 地址（有时称为 “集群 IP”），该 IP 地址由服务代理使用。
```
```
发布服务（服务类型)
对一些应用的某些部分（如前端），可能希望将其暴露给 Kubernetes 集群外部的 IP 地址。

Kubernetes ServiceTypes 允许指定你所需要的 Service 类型，默认是 ClusterIP。

Type 的取值以及行为如下：

ClusterIP：通过集群的内部 IP 暴露服务，选择该值时服务只能够在集群内部访问。 这也是默认的 ServiceType。

NodePort：通过每个节点上的 IP 和静态端口（NodePort）暴露服务。 NodePort 服务会路由到自动创建的 ClusterIP 服务。 通过请求 <节点 IP>:<节点端口>，你可以从集群的外部访问一个 NodePort 服务。

LoadBalancer：使用云提供商的负载均衡器向外部暴露服务。 外部负载均衡器可以将流量路由到自动创建的 NodePort 服务和 ClusterIP 服务上。

ExternalName：通过返回 CNAME 和对应值，可以将服务映射到 externalName 字段的内容（例如，foo.bar.example.com）。 无需创建任何类型代理。
```
#### Pod对象
- 凡是调度，网络，存储，以及安全相关的属性基本上都是Pod级别的

#### 容器 - 隔离与限制
- 容器是一个“单进程”模型
## Others
```
把eBay的一些核心应用从物理机迁移到容器
1，对于应用，它容器化之后，发布和部署更加方便，特别是在扩容的时候更快了。
2. 对于平台，我们用一套平台kubernetes来管理所有的应用，对于硬件资源的利用率得以提高。
所以容器化后，带来的好处是，开发效率的提高，资源利用率的提高。
```

### aws配置
- https://github.com/docker/hub-feedback/issues/1318#issuecomment-396429154 pull images的时候如果403