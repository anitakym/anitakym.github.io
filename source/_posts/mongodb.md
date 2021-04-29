---
title: mongodb
date: 2021-04-23 22:15:30
tags:
---
## Basic

### docs
- https://docs.mongodb.com/guides/
- https://university.mongodb.com/?tck=docs_landing

### intro
- DB-Engines 排名
- 重新定义OLTP数据库 - （tips:OLAP）
- JSON Document 以JSON为数据模型的文档数据库
- MongoDB Inc.
- 建模可选/横向扩展可以支撑很大的数据量和并发
- 社区版（SSPL）/企业版（商业协议）
- 数据容量-理论上没有上限

### history
0.x 2008
1.x 2010 - 支持复制集（高可用）和分片集
2.x 2012 - 数据库功能
3.x 2014 - WiredTiger + 生态
4.x 2018 - 分布式事务支持

#### 闲话
- 竞品：
14年，微软推出了DocumentDB预览版，17年5月升级为Cosmos DB（包含多个数据模型，文档模型成为子集）
MongoDB-易用性！ 稳定性（丢数据，安全，分布式处理能力）？
DocumentDB-Leslie Lamport(对事务的处理，自动索引，PaaS服务)
做成了Windows Azure的一个服务
17年，提供了兼容MongoDB的API
（17年1月，黑客大量袭击了默认安装的MongoDB）

- 人
DoubleCLick原创始人（Dwight Merriman, Kevin Ryan, Eliot Horowitz）
原先想做一个云计算的服务的
然后先搭一个数据库

mongo - humongous - 海量数据库 - 面向集合，模式自由，文档型数据库（Accelerate development, address diverse data sets, and adapt quickly to change with a proven application data platform built around the database most wanted by developers 4 years running.）

PS：SQL是IBM出来的

10gen 在 2009年2月正式开源MongoDB的第一个版本

商业上-资助用户组，对社区的支持，技术支持团队-nice（用户体验）

13年更名 MongoDB公司



### advantage
- 面向开发者的易用&&高效数据库
- 对象模型（Objects=>Database）
- 快速响应业务变化（可动态增加新字段）
  - 多形性:同一个集合中，可以包含不同字段的文档对象
  - 动态性：线上修改数据模式，修改时应用与数据库均无需下线
  - 数据治理：支持使用JSON Schema来规范数据模式。在保证模式灵活动态的前提下，提供数据治理能力