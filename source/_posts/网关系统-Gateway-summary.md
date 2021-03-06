---
title: 网关系统-Gateway-summary
date: 2022-03-10 17:38:05
tags:
---
## why
- 应用稳定性: 如果没办法对单一的模块做熔断、升级、回滚等操作，线上不可控的概率极大 -> 微服务架构
```
通用性的认证、鉴权、限流 -> 微服务-造轮子
业务复杂度上升 -> 域名分配问题
服务使用的语言框架差异 - DevOps 系统
```
- 网关系统 - 通过网关的统一入口来调度各个微服务功能模块，使得每个微服务可以关注于自身的业务功能开发

## what
#### 请求类型
- 静态资源网关 - CSR ｜ SSR
- API网关 - MSA - 统一出入口 - 降低接入和使用成本

#### 功能
- 流量网关 - 安全（黑白名单），分流（负载均衡）
- 业务网关 - 用户（认证，鉴权），服务稳定性（降级，容灾，分流），业务属性灰度（AB test），代理（资源代理，缓存 - 成本高），统一前置（日志，数据校验）

#### 网关基础服务
- 资源分发｜API分发
- 资源缓存模块
- AB TEST模块
- 通用日志模块

#### 统一用户中心系统
- 用户登录，认证等
- 权限系统（RBAC） - 优先级高

#### 物料系统
- DevOps相关

### frameworks
- Nginx+Lua：Open Resty、Abtesting Gateway
- Java：Spring Cloud Gateway
- Go：Janus、Grpc-Gateway
- Node.js：Express Gateway、MicroGateway