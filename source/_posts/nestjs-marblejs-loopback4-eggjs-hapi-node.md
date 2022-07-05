---
title: nestjs-marblejs-loopback4-eggjs-hapi-node
date: 2021-11-19 16:07:59
tags:
---
## Nest
### awesome
- https://docs.nestjs.cn/8/awesome
- https://docs.nestjs.com/
- https://medium.com/monstar-lab-bangladesh-engineering/why-i-choose-nestjs-over-other-node-js-frameworks-6cdbd083ae67
- https://zhuanlan.zhihu.com/p/389639059 - great!!!
- they have cats !!



## Egg

### 日志
- https://eggjs.org/zh-cn/core/logger.html
- egg-logger
- 使用的时候知道什么日志什么意思，接入第三方的日志收集的时候，能对得上就行
- egg-logrotator
- 日志同步写入内存，异步每隔一段时间(默认 1 秒)刷盘


## Hapi
- https://hapi.dev/
- 可靠，安全，可读
- Middleware(express) vs Plugins and Extensions(hapi)
```

Middleware vs Plugins and Extensions
To extend its functionality, Express uses middleware. Middleware essentially is a sequence of functions using callbacks to execute the next function. The issue with this is as your application grows in size and complexity, the order at which middleware executes becomes more crucial and more difficult to maintain. Having a middleware execute before one it is dependant on will cause your application to fail. hapi fixes this issue with its robust plugin and extension system.

Plugins allow you to break your application logic into isolated pieces of business logic, and reusable utilities. Each plugin comes with its own dependencies which are explicitly specified in the plugins themselves. This means you don't have to install dependencies yourself to make your plugins work. You can either add an existing hapi plugin, or write your own. For a more extensive tutorial on plugins, please see the plugins tutorial.

Each request in hapi follows a predefined path, the request lifecycle. hapi has extension points that let you create custom functionality along the lifecycle. Extension points in hapi let you know the precise order at which your application will run. For more info, please see the hapi request lifecycle.
```
- https://hapi.dev/tutorials/expresstohapi/?lang=zh_CN  (express 和 hapi的比较，也是可以怎么从express迁移到hapi)
- hapi其实常拿来和express，koa做比较，没什么最好的，只有最合适的
- https://github.com/vendia/serverless-express
- koa和express可见《nodejsWeb应用开发-精读》