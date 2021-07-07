---
title: redis使用手册-精读
date: 2021-07-02 11:29:03
tags:
---

> 书里面的示例是用python实现的，我这边用node实现了下

## 安装配置

### 参考文档
https://groups.google.com/g/redis-db

### 安装

#### Mac安装：
```
xcode-select --install
git clone https://github.com/antirez/redis.git
cd redis
make
make test
cd src
./redis-server
./redis-cli
```
#### windows
官方不支持，可以用docker(https://hub.docker.com/_/redis/)

#### redis-py
```
pip install redis
python3
>>> from redis import Redis
>>> client = Redis()
>>> client.set("msg","hello world")
>>> client.get("msg)
>>> for i in dir(client)
```

## 数据结构
> 命令COMMAND - https://redis.io/commands

### 字符串
- 文字数据 ｜ 二进制数据 均可
- 制定命名格式 - 提升可读性+避免键名冲突
- 多个字符串键存储相关联的一组数据 - 技术可行，并不最有效
#### SET ｜ GET ｜ GETSET 
NX（只在键不存在的情况下为它设置值） ｜ XX （只在键已经存在的情况下为它设置新值）
#### MSET 
减少网络通信次数，从而减少程序执行多个设置操作的时间
#### MGET
#### MSETNX
只要有一个键有值，会放弃对所有给定键的操作
#### STRLEN
#### GETRANGE
- ```GETRANGE key start end``` 
- 位于start&end的值也包含
#### SETRANGE
- ```SETRANGE key index substitute```
- 自动扩展，空字节填充
#### APPEND
- 键不存在-设置；键存在-追加
#### INCRBY ｜ DECRBY ｜ INCR ｜ DECR ｜ INCRBYFLOAT
可用于计数器 ｜ id生成器 ｜ 限速器


### 散列
- 通过散列键，包相关联的多项数据存储到一个散列中
- eg. 短网址生成程序
- 无序
#### HSET | HSETNX | HGET 
```HSET hash field value```
#### HINCRBY
没有提供减法操作，通过传负数增量来实现
#### HINCRBYFLOAT
counter
#### HSTRLEN ｜ HEXISTS ｜ HDEL ｜ HLEN
login session
#### HMSET ｜ HMGET
#### HKEYS ｜ HVALS ｜ HGETALL
graph 
文章存储
### 字符串键和散列键比较
#### 资源占用
内存&&CPU —— 散列
#### 支持的操作
字符串：SETRANGE｜GETRANGE

#### 过期时间
字符串粒度更细，相比较

### 列表
- list
- 线性有序结构

#### LPUSH ｜ RPUSH ｜ LPUSHX ｜ RPUSHX
- -X 只对已存在对列表执行推入操作
#### LPOP | RPOP | RPOP ｜ RPOPLPUSH
- FIFO 队列
#### LLEN ｜ LINDEX ｜ LRANGE
- 分页
#### LSET ｜ LINSERT ｜ LTRIM ｜ LREM 
- ToDo List
#### BLPOP ｜ BRPOP ｜ BRPOPLPUSH
- 有阻塞功能的消息队列

### 集合
- 非重复元素
- 无序
#### SADD | SREM | SMOVE | SMEMBERS | SCARD | SISMEMBER
- unique count
- tag
- thumb
- vote
- social relationship
#### SRANDMEMBER | SPOP
- 抽奖

#### SINTER | SINTERSTORE | SUNION | SUNIONSTORE | SDIFF | SDIFFSTORE
- 共同关注
- 反向索引构建商品筛选器

### 有序集合
- sorted set

#### ZADD | ZREM | ZSCORE | ZINCRBY | ZCARD | ZRANK | ZREVERANK | ZRANGE | ZREVERANGE
- ZADD - O(M*log(N))
- 排行榜

#### ZRANGEBYSCORE ｜ ZREVERAMGEBYSCORE ｜ ZUNIONSTORE ｜ ZINTERSTORE
- 商品推荐

#### ZRANGEBYLEX ｜ ZRVERANGEBYLEX ｜ ZLEXCOUNT ｜ ZERMRANGEBYLEX
- 自动补全

#### ZPOPMAX ｜ ZPOPMIN ｜ BZPOPMAX ｜ BZPOPMIN 

### HyperLogLog

- 概率算法，对大量元素进行计数，算出近似基数
- 使用固定大小内存
- PFMERGE - HyperLogLog-PFCOUNT
- 可以用于去重
- 基数统计：cardinality of a set is a measure of the "number of elements" of the set
- standard error - 0.81%