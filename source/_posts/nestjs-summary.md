---
title: nestjs-summary
date: 2023-03-10 17:24:59
tags:
---
### doc
- https://docs.nestjs.cn/

#### @nestjs/cli
new | generate

monorepo | multirepo

## 内置框架选择
- fastify - 基准测试 - 性能 - like QPS
- 

### 能力

- IOC：自己实现了模块机制，可以导入导出 provider，实现自动依赖注入，简化了对象的创建
- AOP：抽象了 Guard、Interceptor、Pipe、Exception Filter 这 4 种切面，可以通过切面抽离一些通用逻辑，然后动态添加到某个流程中
- 任意切换底层平台：nest 基于 ts 的 interface 实现了不和任何底层平台耦合，http 可以切换 express 和 fastify，websocket 可以切换 socket.io 和 ws。而且 4 种切面也实现了可以跨 http、websocket、微服务来复用。
