---
title: nestjs-summary
date: 2023-03-10 17:24:59
tags:
---

### github
- 代码拉下来，node 14.X的才能正常install,默认lock文件不ignore(Fix the upstream dependency conflict, or retry
npm ERR! this command with --force or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.)
-  "engines": {
    "node": ">= 16"
  },
- 当您使用 npm v7 及更高版本时，默认情况下，peer 依赖项将自动安装，并在遇到冲突时中止安装并报错。这是为了确保所有依赖项与其 peer 依赖项完全兼容，避免后续的问题

### publish
- 较为完备的多packages的publish脚本
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


### github - examples
- https://github.com/Ignition-Space/fast-gateway/
- https://wanago.io/
- https://github.com/hantsy/nestjs-rest-sample

### 全局模块
- 模块可以通过 @Global 声明为全局的，这样它 exports 的 provider 就可以在各处使用了，不需要 imports。


### 生命周期

provider、controller、module 都支持启动和销毁的生命周期函数，这些生命周期函数都支持 async 的方式。

可以在其中做一些初始化、销毁的逻辑，比如 onApplicationShutwon 里通过 moduleRef.get 取出一些 provider，执行关闭连接等销毁逻辑。

全局模块、生命周期、moduleRef 都是 Nest 很常用的功能。