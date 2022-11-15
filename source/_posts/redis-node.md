---
title: redis-node
date: 2021-07-03 13:34:49
tags:
---
> 官网指南： redis.js.org/
### cache.js
```
// SET ｜ GET （缓存的数据，字符串键）
// 字符串键
```

### redisInsight
- 官方可视化管理工具

### redisMod
```
RediSearch：一个功能齐全的搜索引擎
RedisJSON：对JSON类型的原生支持
RedisTimeSeries：时序数据库支持
RedisGraph：图数据库支持
RedisBloom：概率性数据的原生支持
RedisGears：可编程的数据处理
RedisAI：机器学习的实时模型管理和部署
```
docker pull redislabs/redismod:preview
docker run -p 6379:6379 --name redismod -v /mydata/redismod/data:/data -d redislabs/redismod:preview