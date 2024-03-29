---
title: 网络协议-summary
date: 2022-08-11 16:57:02
tags:
---
### 容器网络

#### 容器的思想
- 变成软件交付的集装箱
- 一是打包
- 二是标准

#### 封闭的环境：
1. 看起来是隔离的技术：namespace，也即每个 namespace 中的应用看到的是不同的 IP 地址、用户空间、程号等。
2. 用起来是隔离的技术：cgroup，也即明明整台机器有很多的 CPU、内存，而一个应用只能用其中的一部分。


#### 标准：镜像


#### 命名空间（namespace）（ip netns）
至此为止，基于网络 namespace 的路由器实现完毕。

#### 机制网络（cgroup）
- cgroup 全称 control groups，是 Linux 内核提供的一种可以限制、隔离进程使用的资源机制。

- net_cls，这个子系统使用等级识别符（classid）标记网络数据包，可允许 Linux 流量控制程序（tc）识别从具体 cgroup 中生成的数据包。cgroup 提供了一个虚拟文件系统，作为进行分组管理和各子系统设置的用户接口。要使用 cgroup，必须挂载 cgroup 文件系统，一般情况下都是挂载到 /sys/fs/cgroup 目录下。


- 容器是一种比虚拟机更加轻量级的隔离方式，主要通过 namespace 和 cgroup 技术进行资源的隔离，namespace 用于负责看起来隔离，cgroup 用于负责用起来隔离。

- 容器网络连接到物理网络的方式和虚拟机很像，通过桥接的方式实现一台物理机上的容器进行相互访问，如果要访问外网，最简单的方式还是通过 NAT。



### 网络基础
- 寻址和路由 ｜ 数据链路 ｜ 分片 ｜ 序列码 ｜ 封装 ｜ 拥塞控制 
- 错误检测和校正 ｜ 数据重发 ｜ 重组

#### 协议
- 解决如何的问题
- 不同协议处理不同层次的问题
- 使用相同的协议
- ISO - open system interconnection  reference model
- OSI｜Rmodel
- ISP｜ IEC 7489-1
- 主机层 - 应用，表示，会话，传输
- 网络各个节点之间
