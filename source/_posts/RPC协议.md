---
title: RPC协议
date: 2021-11-05 14:04:56
tags:
---

> remote procedure call 远程过程调用

## RPC协议（跨语言类）
- ONC RPC
- （XML） SOAP
- （JSON）RESTful
- Hessian2

> 二进制传输性能好，难以跨语言；文本类的则相反；

## 模式演变
- 客户端服务器模式
- 微服务

## 对RPC框架的要求
- 传输性能
- 跨语言
- 严谨且灵活（添加字段不需要重新编译发布程序）
- 服务发现，服务治理（Dubbo ｜ Spring Cloud）

## GRPC
### 二进制序列化协议
- Protocol Buffers
- .proto
- 压缩效率很高

### 网络传输
- Java - Netty(高效的基于异步IO的网络传输框架)
- 服务方法 - 单向RPC ｜ 服务端流式RPC ｜ 客户端流失RPC ｜ 双向流式RPC

### 服务发现(Discovery Service)与治理
- 负载均衡 - LVS HAProxy Nginx
- Envoy - GRPC
- 配置 - listener ｜ endpoint ｜ cluster ｜ route
- 注册治理中心
- 未来服务治理的趋势 - Service Mesh(基于Envoy)

#### 注册治理中心
- https://mp.weixin.qq.com/s/IhPfssotldNWn9GF4Dx6qg - 腾讯注册中心演进及性能优化实践
