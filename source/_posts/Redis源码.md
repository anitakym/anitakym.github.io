---
title: Redis源码
date: 2021-07-27 10:32:53
tags:
---
#### C语言 - 学习素材
- 单测
- 命名非常规范
#### 设计与实现
- 单机键值数据库
- 分布式系统

#### 代码阅读
- 整体上掌握结构
- 要有目标牵引和原理支撑
- 先主线逻辑再分支细节

## 整体架构
### Redis
#### deps
- 可独立于src目录下的功能源码进行编译
#### src
- C语言风格，不同模块间不再设置目录分隔，而是通过头文件包含来相互调用
#### tests
> Tcl语言编写
- 单元测试
- Redis Cluster功能测试
- 哨兵功能测试 - sentinel
- 主从复制功能测试 - integration
#### utils
- create-cluster - 创建集群工具
- hashtable - rehash过程可视化
- hyperloglog - hyperloglog误差率计算和展示
- lru - LRU算法效果展示

### 服务器实例

### 数据库数据类型与操作

#### Redis如何优化内存使用
- 内存分配
- 内存回收
- 数据替换

## 可靠性
- 对数据做持久化保存 -> 内存快找RDB｜AOF日志
- 主从复制机制 -> 提供故障恢复功能 - replication.c

## 扩展性
- Redis Cluster

## others
### dragonfly
- https://github.com/dragonflydb/dragonfly