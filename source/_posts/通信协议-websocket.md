---
title: 通信协议-websocket
date: 2021-09-13 16:44:34
tags:
---
> 还是说文解字，用于“通信”的“协议”； web 指运行在web（也就是通常我们广义的理解的话 HTTP那一层的） 上；

### 先明确几个定义

#### “请求-应答”的通信模式-半双工
HTTP是这个模式，问题在于同一时刻只能单方向动作；服务器被动响应；

（HTTP/2 ｜ HTTP/3  ———— Stream｜Server Push）

#### 轮询-polling
问题： 消耗带宽和CPU资源

#### long-polling
- 发出大量请求
- 在某个时间间隔内进行AJAX调用
- 关键是什么？
```
保证核心操作的简单，快

不要只使用setInterval - 没有考虑到请求需要时间的事实
在当前请求完成后立即为下一个请求启动一个定时器（在函数的末尾为下一个请求SetTimeout）
```



### Websocket
- HTML5规范出来的，RFC6455
- 全双工，服务器和客户端可以随时发送数据
- 二进制帧结构，语法语义与HTTP不兼容

#### 协议
- IETF 
#### API
- W3C
#### 服务发现
URI：wss|ws 表明协议

#### 默认端口
80｜443

#### 应用场景
实时通信
客户端需要不断更新的部分

#### 帧结构
- 指路wiki:https://zh.wikipedia.org/wiki/WebSocket
- 指路RFC：https://datatracker.ietf.org/doc/html/rfc6455
- 可以Wireshark抓包试一下，看看就有感觉了（N年前网络实验课啥都抓一下后遗症。。。
- 抓出来的报文，Masking-key 异或下，就可以转出来明文了

#### handshake
- "Connection:Upgrade" "Upgrade:websocket" (HTTP 协议升级)
- "Sec-WebSocket-Key" "Sec-WebSocket-Version"(Challenge，防止HTTP被识别为WebSocket)
- 服务器返回一个"101 Switching Protocols"响应报文，"Sec-WebSocket-Accept"-由服务器对前面客户端发送的Sec-WebSocket-Key进行确认和加密后的结果，相当于一次验证，以帮助客户端确信对方是真实可用的WebSocket服务器
- https://www.yuque.com/fe9/basic/101
### case
#### WebSocket is closed before the connection is established.

If you go to http://jsbin.com/ekusep/6/edit and view the JavaScript console you'll see the 'WebSocket is closed before the connection is established' logged. I've tested this in Chrome.
In this code what it means is that ws.close() was called (by user code) before the connection was even given a chance to be established.
So, the cause of this error is if code attempts to close the WebSocket connection before it's had a chance to actually connect.

#### send()
- 消息类型
- 字符串 ｜ Blob ｜ ArrayBuffer
- binaryType - 初始值为blob,可以设置为arraybuffer
### 拓展理解
- TCP Socket
#### SSE - Server-Sent Events
- https://developer.mozilla.org/zh-CN/docs/Web/API/Server-sent_events
- 服务器推送信息
- 服务器向客户端声明 - 接下来要发送的是流信息 streaming
- 基于HTTP协议
- IE/Edge低版本不支持
- 单向通道
- https://caniuse.com/eventsource

content-type:
text/event-stream

`text/event-stream`是一种MIME类型，它被用于服务器发送事件(SSE，Server-Sent Events)协议中。在这个协议中，通过一个HTTP连接，服务器可以发送到客户端的一连串的事件。与Websockets相比，SSE是单向的，只允许服务器向客户端发送消息。

每个事件以`data: `开始，后面跟着消息的内容，然后是两个换行符来表示消息的结束。服务器可以发送任意多的事件，只要连接保持打开状态。

这种类型的通信特别适合于服务器需要实时，持续地发送更新（例如股票价格更新，新闻滚动，实时计分等）给客户端，但客户端不需要频繁地向服务器发送数据的场景。

使用`text/event-stream`的服务器发送事件(SSE)是HTML5引入的一个标准，被所有现代浏览器支持。