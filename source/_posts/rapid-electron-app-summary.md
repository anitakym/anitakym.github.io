---
title: rapid-electron-app-summary
date: 2023-08-15 10:18:45
tags:
---
```
npm ERR! command sh -c node install.js
npm ERR! RequestError: connect ETIMEDOUT 20.205.243.166:443
npm ERR!     at ClientRequest.<anonymous> (/Users/kuangyimin/rapid.app/node_modules/got/dist/source/core/index.js:970:111)
npm ERR!     at Object.onceWrapper (node:events:626:26)
npm ERR!     at ClientRequest.emit (node:events:523:35)
npm ERR!     at origin.emit (/Users/kuangyimin/rapid.app/node_modules/@szmarczak/http-timer/dist/source/index.js:43:20)
npm ERR!     at TLSSocket.socketErrorListener (node:_http_client:495:9)
npm ERR!     at TLSSocket.emit (node:events:511:28)
npm ERR!     at emitErrorNT (node:internal/streams/destroy:151:8)
npm ERR!     at emitErrorCloseNT (node:internal/streams/destroy:116:3)
npm ERR!     at process.processTicksAndRejections (node:internal/process/task_queues:82:21)
npm ERR!     at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1571:16)
```
- electron 安装的网络问题
- electron的install.js
- 处理下网络代理即可
- install.js -> @electron/get -> got 


### https://www.electronforge.io/
- electronforge
- Electron Forge 是打包和发布 Electron 应用程序的一体化工具。它结合了许多单一用途的软件包，创建了一个完整的构建管道，开箱即用，包括代码签名、安装程序和工件发布。对于高级工作流程，可通过其插件应用程序接口（Plugin API）在 Forge 生命周期中添加自定义构建逻辑。
- 基本上在electron应用开发中的工程化和发布问题，都一站式解决了