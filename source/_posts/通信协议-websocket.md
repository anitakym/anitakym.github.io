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

### websocket
- HTML5规范出来的，RFC6455
- 全双工，服务器和客户端可以随时发送数据
- 二进制帧结构，语法语义与HTTP不兼容
#### 服务发现
URI：wss|ws 表明协议

#### 默认端口
80｜443

#### 应用场景
实时通信

#### 帧结构
- 指路wiki:https://zh.wikipedia.org/wiki/WebSocket
- 指路RFC：https://datatracker.ietf.org/doc/html/rfc6455
- 可以Wireshark抓包试一下，看看就有感觉了（N年前网络实验课啥都抓一下后遗症。。。
- 抓出来的报文，Masking-key 异或下，就可以转出来明文了

#### handshake
- "Connection:Upgrade" "Upgrade:websocket" (HTTP 协议升级)
- "Sec-WebSocket-Key" "Sec-WebSocket-Version"(Challenge，防止HTTP被识别为WebSocket)
- 服务器返回一个"101 Switching Protocols"响应报文，"Sec-WebSocket-Accept"

### case
#### WebSocket is closed before the connection is established.

If you go to http://jsbin.com/ekusep/6/edit and view the JavaScript console you'll see the 'WebSocket is closed before the connection is established' logged. I've tested this in Chrome.
In this code what it means is that ws.close() was called (by user code) before the connection was even given a chance to be established.
So, the cause of this error is if code attempts to close the WebSocket connection before it's had a chance to actually connect.
### 拓展理解
- TCP Socket
#### SSE - Server-Sent Events
- https://developer.mozilla.org/zh-CN/docs/Web/API/Server-sent_events
- 服务器推送信息
- 服务器向客户端声明 - 接下来要发送的是流信息 streaming
- 基于HTTP协议
- IE/Edge不支持
- 单向通道