---
title: nodejs-why-and-how-and-what
date: 2022-01-29 21:52:08
tags:
---

- 性能，并发性，可用性，可靠性，可扩展性
- 从开始设计，用于构建实时和并发系统
- 发展，改进中

## arch
- the node.js system
- application - v8 - javascript engine
- node.js bindings - node api - os operation
- libuv - asysnchronous I/O - event queue - event loop - worker threads - file system|network|process - blocking operation|execute callback
- nodejs线程 | c++线程
## nodejs内置模块

### EventEmitter
- 观察者模式
    - addEventListener | removeEventListener
    - 调用|抛事件
    - 谁在听 | 听没听
## 异步
### 非阻塞I/O
- Input/Output 系统的输入和输出
- 阻塞？ 系统接收输入到再输出期间，能否接收其它输入

### callback
- func格式规范 - error-first！！！ | node-style callback
- 异步流程控制 - 回调地狱 | 异步并发（A&&B => Do C）- 就要加计数器等一堆逻辑来达成
- history - package-async.js | thunk-编程范式

### throw Error
- 全局的会导致程序崩溃
- call stack 调用栈 | try catch 如果不在包裹内，则无法捕捉
- 事件循环 - setTimeout | 注意捕捉范围
### 事件循环


### Promise

### async/await



## source code
#### 内置模块
- os.js - internalBinding - node_os.cc - libuv
- v8
- 


## 其他语言
### golang
- coroutines
### erlang
- 抢占式调度
