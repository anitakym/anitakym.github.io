---
title: task-job-schedule
date: 2024-04-22 22:33:43
tags:
---
主流 - 单机|分布式 - 定时任务

XXL-JOB
Elastic-Job
SpringTask
ScheduledThreadPoolExecutor

解决什么问题

统计分析类场景 - 性能优化 - 预计算

全量预计算
存量预计算+增量即席计算


Redis 存取

跟SpringTask一样, ScheduledThreadPoolExecutor也是Java内的工具,所以它本身并不支持Node.js。 Node.js有自己的处理异步任务和定时任务的机制和库。

Node.js有一些类似的库，可以创建和管理定时任务，比如node-cron、node-schedule和bull等。这些库都可以实现类似ScheduledThreadPoolExecutor的功能。

Elastic-Job是阿里巴巴开源的一个分布式调度解决方案，主要通过Java进行开发，对于其他语言的支持主要是通过其提供的RESTful API来实现。

对于Node.js，你可以通过调用这些RESTful API来与Elastic-Job进行交互，但是它并没有专门为Node.js提供客户端库。

所以，虽然不能直接说Elastic-Job支持Node.js，但是Node.js应用程序是可以与之进行交互的。

XL-JOB是一个轻量级分布式任务调度框架，它主要是基于Java开发的。根据官方文档，XXL-JOB提供了多种任务模式，包括Bean模式，GLUE模式（Java，Golang，PHP，NodeJS，Python，Shell，PowerShell）。

所以，针对你的问题，XXL-JOB是支持Node.js的。你可以在XXL-JOB的调度平台上编写和管理Node.js任务。然后通过XXL-JOB提供的客户端，运行和调度这些Node.js任务。