---
title: socket-io
date: 2024-10-12 15:02:51
tags:
---
Socket.IO 是一个流行的库，它简化了在浏览器和服务器之间实现实时通信。Socket.IO 通过抽象出底层的传输协议，使开发者能够在客户端和服务器端之间创建双向通信，不必关心具体使用的是 WebSocket 还是 Long Polling。

Socket.IO 在底层会首先尝试使用 WebSocket 协议，如果不支持 WebSocket，则会退而使用 Long Polling。这种回退机制使得 Socket.IO 在各种环境下都能稳定运行，同时也提供了丰富的 API 用于实时通信。

安装
首先，我们需要安装 Socket.IO：

sh
# 安装服务器端的 Socket.IO
npm install socket.io

# 安装客户端的 Socket.IO
npm install socket.io-client
示例代码
服务器端（Node.js + Express 示例）
首先，创建一个简单的服务器端，它接受来自客户端的连接并发送和接收消息。

javascript
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', (socket) => {
  console.log('a user connected');

  // 接收客户端的消息
  socket.on('chat message', (msg) => {
    console.log('message: ' + msg);
    // 将消息发送给所有连接的客户端
    io.emit('chat message', msg);
  });

  socket.on('disconnect', () => {
    console.log('user disconnected');
  });
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
客户端（HTML + JavaScript 示例）
接着，创建一个简单的客户端，它连接到 Socket.IO 服务器并发送和接收消息。

html
<!DOCTYPE html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      ul { list-style-type: none; margin: 0; padding: 0; }
      li { padding: 8px; background: #f9f9f9; margin-bottom: 5px; border: 1px solid #ddd; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; display: flex; }
      input { border: none; padding: 10px; flex-grow: 1; }
      button { width: 100px; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form id="form" action="">
      <input id="input" autocomplete="off" /><button>Send</button>
    </form>
  
    <script src="/socket.io/socket.io.js"></script>
    <script>
      const socket = io();

      const form = document.getElementById('form');
      const input = document.getElementById('input');
      const messages = document.getElementById('messages');

      form.addEventListener('submit', function(e) {
        e.preventDefault();
        if (input.value) {
          socket.emit('chat message', input.value);
          input.value = '';
        }
      });

      socket.on('chat message', function(msg) {
        const item = document.createElement('li');
        item.textContent = msg;
        messages.appendChild(item);
        window.scrollTo(0, document.body.scrollHeight);
      });
    </script>
  </body>
</html>
解释
服务器端：

express 创建一个 HTTP 服务器。
socket.io 包含的 Server 类启动一个新的 Socket.IO 服务器实例连接到 HTTP 服务器。
io.on('connection', (socket) => {...})：当一个新客户端连接时，该块代码将被执行。每个 socket 实例代表一个客户端连接。
socket.on('chat message', (msg) => {...})：监听来自客户端的消息事件。
io.emit('chat message', msg)：将接收到的消息广播给所有连接的客户端。
客户端：

在 <script src="/socket.io/socket.io.js"></script> 中加载客户端的 Socket.IO 脚本。
io() 初始化连接到服务器。
监听和发送消息。每当用户在表单中提交消息时，消息会通过 socket 发送到服务器。收到服务器消息时，会将消息添加到显示列表中。
优点
自动降级：Socket.IO 会自动选择可用的最佳传输协议（WebSocket 优先，其次是 HTTP 长轮询等）。
可靠性：提供自动重连接、心跳检测等机制保证连接可靠。
API 简单：强大的功能通过简单的 API 实现，非常适合快速开发实时应用。
这个简单的示例展示了如何使用 Socket.IO 创建实时的客户端与服务器通信。实时通信可以应用在如聊天应用、实时通知、多人协作等各种场景。