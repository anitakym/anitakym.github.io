---
title: docker-node-k8s项目实践总结
date: 2021-04-03 12:21:24
tags:
---
> docker - 容器技术 - 在当前操作系统内运行一个专用的操作系统环境
> 保持环境的一致性（开发，生产）
> kubernetes - 容器编排系统 - 管理多个Docker容器（管理Docker的生命周期和扩展Docker容器的规模）
> 特性和API会过时，但通用的概念不会;概念及特定语言的相关框架的实现;对内核的扩展，包含一些现成的模块和功能
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
- `pm2 --no-daemon`命令表示以非守护进程的方式启动pm2进程。在这种方式下，pm2进程会被启动在前台，并会将日志输出到控制台，同时终端窗口关闭后pm2进程也会随之退出。这种方式通常用于调试以及在Docker等容器环境下运行pm2进程。如果要停止以非守护进程的方式启动的pm2进程，只需要在终端窗口中按下 `Ctrl+C` 即可
- Docker 要求内部服务进程在前台模式下运行
```
- 如果在进程管理器中运行 Node.js 应用程序而不使用前台模式，进程管理器会不断启动新的进程。这是因为进程管理器无法监控后台进程的运行状况，因此它无法保证在某个进程失败时立即启动另一个进程。相反，在前台模式下，进程管理器可以检测到进程是否崩溃并立即启动另一个进程，从而保持应用程序的可用性。因此，在使用 systemd、supervisord 等进程管理器时，建议始终将 Node.js 应用程序配置为前台模式运行。
- 在使用 pm2 进行 Node.js 应用程序的进程管理时，并不要求应用程序必须以前台模式运行。相反，pm2 会将 Node.js 应用程序从前台模式转换为后台模式并启动进程，以便进程管理器可以在应用程序崩溃时根据需要自动重启应用程序。这样，即使某个进程崩溃，pm2 也可以自动将其重启，从而保持应用程序的可用性。因此，在使用 pm2 时，可以将 Node.js 应用程序设置为后台模式运行，以提高系统的稳定性。
```
```
Docker 在运行容器时会启动一个 init 进程，这个进程负责容器内的进程管理和信号转发，这个 init 进程的子进程就是我们在容器内启动的服务进程。在默认情况下，Docker 要求容器内的服务进程必须以前台模式运行，也就是说，服务进程必须在前台运行，并将进程的标准输入、标准输出和标准错误输出流与 Docker 主机的标准输入输出流进行绑定。这样，Docker 主机就可以通过控制台来进行服务进程的操作和监控，比如查看进程输出信息、向服务进程发送中断信号等。

如果服务进程以后台模式运行，也就是不在前台运行，那么这个服务进程的标准输入、标准输出和标准错误输出流就无法与 Docker 主机的标准输入输出流绑定在一起，这样 Docker 主机就无法进行服务进程的管理和监控，也就无法对服务进程进行重启、停止等操作，这对于容器的运维和管理带来了很大的挑战，因此 Docker 要求服务进程必须在前台模式下运行。
```
### 前台和后台模式
- 后台守护进程和前台进程
Node.js 在 Linux/Unix 系统中可以运行在前台和后台两种模式下。在前台模式下，Node.js 进程直接运行在当前终端会话中，并且输出日志信息到终端。在后台模式下，Node.js 进程运行在后台，并且它的输出通常被重定向到文件或其他设备上。
下面是一个使用两种模式运行 Node.js 的示例：
在前台模式下运行 Node.js：
```
$ node app.js
```
在后台模式下运行 Node.js：
```
$ nohup node app.js > app.log &
```
在以上的命令中，使用了 `nohup` 命令来运行 Node.js 进程，并且将输出日志到命名为 `app.log` 的文件中。同时，使用 `&` 符号使 Node.js 进程在后台运行。
需要注意的是，在生产环境中，通常会使用像 PM2 或者 Supervisord 这样的进程管理工具来管理 Node.js 应用程序，并确保它们在后台运行时能够自动重启、监控和处理错误。
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


### 系统资源监控工具
brew install htop

### dumb-init
dumb-init是一个简单的init系统，用于管理容器内的多个进程。它主要解决了在Docker和Kubernetes等容器环境中管理进程的问题。

在容器中，通常会运行多个进程，例如一个Web服务器和一个后台守护进程。如果不使用dumb-init这样的init系统，当容器的入口点进程（entrypoint）退出时，容器中的所有进程都将被杀死，而无法进行正常的清理操作。

dumb-init可以作为容器中的入口点进程，并作为所有其他进程的父进程。当子进程退出时，dumb-init会重新注册SIGTERM和SIGINT信号，并将其发送给所有子进程，以便它们能够优雅地退出。

dumb-init还可以设置最大进程数、ulimit参数等，以帮助管理容器内的进程。

Dockerfile
```
RUN curl -L -o /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64
RUN chmod +x /usr/local/bin/dumb-init
ENTRYPOINT ["dumb-init", "--"]
CMD ["/path/to/your/program", "-arg1", "-arg2", ...]
```

### 使用外部代理进行监测和缓存
- 虽然nodejs服务器可以作为 HTTP服务器或 HTTP2服务器使用，但建议 将你的服务器放在 HTTP代理（如 Nginx）或 HTTP2代理（如 Envoy）后面。这样你就可以管理缓存，将日志文件集中化、标准化，并与你的监控系 统集成，以监测nodejs应用的健康和性能。

### child_process




### cluster