---
title: mongodb
date: 2021-04-23 22:15:30
tags:
---
## Basic

### docs
- https://docs.mongodb.com/guides/
- https://university.mongodb.com/?tck=docs_landing
- 中文社区-https://mongoing.com/

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

### advantage
- 面向开发者的易用&&高效数据库
- 对象模型（Objects=>Database）
- 快速响应业务变化（可动态增加新字段）
  - 多形性:同一个集合中，可以包含不同字段的文档对象
  - 动态性：线上修改数据模式，修改时应用与数据库均无需下线
  - 数据治理：支持使用JSON Schema来规范数据模式。在保证模式灵活动态的前提下，提供数据治理能力

### 
