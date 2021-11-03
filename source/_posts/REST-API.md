---
title: REST-API
date: 2021-04-27 16:51:14
tags:
---


### 面临的挑战
（David Mckenna）REST 面临的挑战：
- 反向 API
  - Webhooks | WebSocket | SSE(服务器发送事件)
- 事件驱动
  - Kafka | RabbitMQ
- gRPC
- GraphQL(Facebook)
- OData(Microsoft)
- IoT
  - MQTT
  - AMQP

具体见下面文章：
https://dzone.com/articles/api-is-dead-long-live-the-apis
中文翻译：https://time.geekbang.org/column/article/192032




### 各家API查询
https://www.programmableweb.com/apis/directory


## 接口设计

### MECE
- 分析问题时
- Mutually Exclusive and Collectively Exhaustive
- 无依赖关系，相互独立
- 穷举
- 避免需求膨胀和过度设计

### 命名明确，语义

### 接口的职责 - 每个接口要做的事 => 单一，独立，完整

### 依赖 （减少，如果有，得做好声明）

### Robust （即使没按约定规范来，也不容易出错）

### 面向对象设计5原则
- SOLID