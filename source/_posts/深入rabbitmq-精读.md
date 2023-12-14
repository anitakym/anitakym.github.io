---
title: 深入rabbitmq-精读
date: 2021-06-30 19:03:13
tags:
---
### 私有化部署web端
#### connections:
- virtual hostname(Overview)
- node(Overview) 
- user name(Overview)
- state(Overview)
- ssl/tls(Details)
- protocol(Details) - AMQP 0-9-1	
- channels(Details)
- from client

#### amqp
- https://www.npmjs.com/package/amqplib (AMQP 0-9-1 library and client for Node.JS)
- 

### 流量削峰 - 容器化，扩容消费
### 应用解耦 - 恢复后消费

### test-demo
- rabbitmq,带management的，docker desktop
- 15672 管理界面
- 5672 mq服务