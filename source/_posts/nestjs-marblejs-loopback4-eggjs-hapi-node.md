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
### 核心思想
- https://www.yuque.com/antfe/featured/gf0y3y

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

- v17是个比较大的不兼容的更新
- https://github.com/hapijs/hapi/issues/3658  - 17.0.0 Release Notes
- breaking changes | migration checklist
```
17.0.0
Release Notesadditional information
breaking changes
#3665
Rename route 'config' with 'options'
#3663
Loosen sample and modify peer validator in the routeBase schema
#3662
prerequisite returning empty string yields null on the pre object of request
#3658
17.0.0 Release Notes
#3657
Update hapijs/vise to 3.0.0 from 2.0.2
#3656
Update hapijs/topo to 3.0.0 from 2.0.2
#3655
Update hapijs/podium to 3.1.2 from 1.3.0
#3653
Update hapijs/nigel to 3.0.0 from 2.0.2
#3652
Update hapijs/mimos to 4.0.0 from 3.0.3
#3651
Update jshttp/mime-db to 1.31.0 from 1.29.0
#3650
Update hueniverse/iron to 5.0.4 from 4.0.5
#3649
Update hapijs/hoek to 5.0.2 from 4.2.0
#3648
Update hapijs/cryptiles to 4.1.0 from 3.1.2
#3647
Update hapijs/content to 4.0.3 from 3.0.6
#3646
Update hapijs/catbox-memory to 3.1.1 from 2.0.4
#3645
Update hapijs/catbox to 10.0.2 from 7.1.5
#3644
Update hapijs/call to 5.0.1 from 4.0.2
#3643
Update hapijs/boom to 7.1.1 from 5.2.0
#3642
Update hapijs/b64 to 4.0.0 from 3.0.2
#3641
Update hapijs/ammo to 3.0.0 from 2.0.4
#3640
Update hapijs/accept to 3.0.2 from 2.1.4
#3639
Update hapijs/statehood to 6.0.5 from 5.0.3
#3638
Update hapijs/shot to 4.0.3 from 3.4.2
#3637
Update hapijs/heavy to 6.0.0 from 4.0.4
#3636
Update hapijs/wreck to 14.0.2 from 13.0.3
#3635
Expose payload and credentials to dynamic scopes
#3634
onCredentials ext point
#3633
Separate authorization (403) from authentication (401)
#3632
Add negative test on registering plugin twice without `once`
#3631
When event data is an error, field name is error
```