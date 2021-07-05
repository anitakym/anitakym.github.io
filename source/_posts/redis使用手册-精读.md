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

- eg. 短网址生成程序
#### HSET | HSETNX | HGET 
```HSET hash field value```
#### HINCRBY
#### HINCRBYFLOAT

