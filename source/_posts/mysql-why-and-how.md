---
title: mysql-why-and-how
date: 2022-11-14 11:39:03
tags:
---

> backend - storage - practice
#### concept
- mysql数据库实例 - 代表着mysql服务器程序的进程
- 进程ID - PID

## MySQL - 高可用，分片问题

#### NewSQL
- Google - Cloud Spanner
- OceanBase
- CockroachDB - 小强数据库

#### No SQL
性能好，存储结构简单-容易组成分布式集群，水平扩展，高可用，高可靠，不支持SQL
- Redis
- KV 存储系统

## 数据库扩展
- 读操作是最耗数据CPU的操作 => 读写分离CQRS-Command and Query Responsibility Segregation
- https://www.slideshare.net/planetcassandra/codecentric-ag-cqrs-and-event-sourcing-applications-with-cassandra