---
title: nodejs底层
date: 2023-02-06 11:23:21
tags:
---
- 之前博文链接 - Libuv-summary



## http模块
#### http协议
- https://developer.mozilla.org/en-US/docs/Web/HTTP
```
Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML. 
It was designed for communication between web browsers and web servers, but it can also be used for other purposes. 
HTTP follows a classical client-server model, with a client opening a connection to make a request, then waiting until it receives a response. 
HTTP is a stateless protocol, meaning that the server does not keep any data (state) between two requests.
```
- 总结下：
- 应用层协议
- 客户端-服务端模型
- 无状态协议

#### http解析器
- https://github.com/nodejs/llhttp
- 钩子函数
- https://github.com/nodejs/llhttp/blob/main/src/native/api.h

#### http服务器
- 1.通过net模块启动一个TCP服务器
- 2.通过llhttp来解析TCP服务器上收到的http数据

- 管道化（1.0 2.0 3.0）- 在同一个TCP连接中并发发送多个请求，但是响应需要按需返回

- Http Connect方法 - 通过connect让http代理服务器转发客户端的tcp流量到另一个真正的服务器中

- 协议升级（WS）- 通过http协议协商升级到另一个通信协议，后续就可以使用新的协议进行通信了


#### HTTP客户端
- 请求Agent（对TCP连接进行了池化管理）（key的计算 + 创建一个socket， 使用连接池）


## worker_threads 模块
- 工作线程对于执行 CPU 密集型的 JavaScript 操作很有用。 它们对 I/O 密集型的工作帮助不大。 Node.js 内置的异步 I/O 操作比工作线程更高效。
- http://nodejs.cn/api/worker_threads.html
- vscode - 