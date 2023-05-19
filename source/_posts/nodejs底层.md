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


## cases

- V8 和 libuv 来实现一个 APM（应用性能监控）watchdog  -> 解决单线程限制。
- 建立一个与 Node.js 主线程并行的 V8 工作线程。

以下是一些步骤和建议来实现一种 APM watchdog：

1. 使用 V8 的 Isolate::New 和 Locker 构造新的 Isolate，以提供一个可以在新线程中执行 JavaScript 的隔离环境。为 V8 工作线程创建一个新的 Isolate，并与 Node.js主线程进行隔离。
2. 使用 V8 的 Platform::CallOnBackgroundThread 方法，使得 V8 可以将任务传送到后台线程运行，用于提供多线程的性能监控。
3. 使用 libuv 中的 uv_loop_new 和 uv_async_send 方法，他们提供简化跨线程通信的能力。用 libuv 来创建一个事件循环，为事件驱动的异步调度提供支持。
4. 设计一个来自于主线程的通知机制。当主线程发现超时或者其他错误发生时，向工作线程发送通知。
5. 使用 V8 的 CPUProfiler API 来抓取 CPU profile，它可以在工作线程和主线程都使用。这将帮助查詢那些很可能会导致应用程序性能降低的代码片段。
6. 设计策略以避免争用条件或数据不一致，并确保应用程序代码的线程安全。当涉及访问多线程共享资源时，请选择互斥锁，读写锁等同步原语。
7. 在你需要的时候，定期启动或暂停 watchdog 线程以汇报其性能数据。可以通过 HTTP 服务暴露相应的性能数据。

