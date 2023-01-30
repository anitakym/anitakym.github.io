---
title: node-benchmark
date: 2021-06-22 11:04:59
tags:
---

### node
node的benchmark写的还是非常值得学习的


### 项目经验
- 会做redis的基准测试方案
- ```redis-benchmark -h [目标机的IP] -p [目标机的redis端口号] -a [目标机redis密码,可省略] –q```
- 精简测试｜pipeline测试｜随机key测试
- QPS（request per second）的情况


### 基础知识
- QPS - 每秒查询率 fetches/sec 每秒响应的请求数，也就是最大吞吐能力
- TPS - 吞吐量 - 单位时间内能处理的数量
- 并发：一段时间访问的大量用户的请求
- 并行：同一时刻的大量的用户请求
- 峰值时间的每秒请求 / 单台的QPS = 机器数量