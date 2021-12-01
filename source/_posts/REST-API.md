---
title: REST-API
date: 2021-04-27 16:51:14
tags:
---

### basic
- 表述性状态转移
- 一切看作资源
- 资源 - CURD
- 使用URI来定位资源
- 使用HTTP动词来操作资源
- 视图函数的URI不应该包含动词

### 理论/实践
- 内部API - 业务逻辑负责
- 开放API - 标准REST


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


## Django

### 蓝图分离视图函数的缺陷