---
title: node-项目应用
date: 2021-04-30 23:26:27
tags:
---

> 事件驱动学习; 很多东西，不同阶段再去听去看，会有不同收获，因为基础认知不同，才能理解到一些细节
### 三句basic 说明
- Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.
- As an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications. 
- Almost no function in Node.js directly performs I/O, so the process never blocks except when the I/O is performed using synchronous methods of Node.js standard library. 

### usage
- web应用场景
- SSR-搜索引擎优化，首屏速度
- 前后端同构（PDF预览打印场景
```
前后端同构
浏览器端 && nodejs端 => 同构代码
ReactDomServer.renderToString()
VueServerRenderer.renderToString()
R&V最大难题在于数据部分

同构的core
- 注重职责分离

```
- 构建工具（早期的 gulp,webpack，后面不用说了，奏是这个生态）
- Backend for Frontend(HTTP, RPC调用)
## basic

### global
- https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame
- setImmediate

### __filename | __dirname
### Err
#### EMFILE - Too many open files

### Process
- argv
- env
- kill 
- exit
- hrtime
- cpuUsage
- memoryUsage

### Module
#### browser
- <script />
- 脚本加载顺序 
- 脚本之间逻辑调用，借助全局变量

#### commonJS
- 也影响了browser端


#### Doc
- http://nodejs.cn/api/process.html
#### Details
- process 对象是 EventEmitter 的实例
- doc
```
'beforeExit' 事件#
中英对照

新增于: v0.11.12
当 Node.js 清空其事件循环并且没有额外的工作要安排时，则会触发 'beforeExit' 事件。 通常情况下，当没有工作要调度时，Node.js 进程会退出，但是注册在 'beforeExit' 事件上的监听器可以进行异步的调用，从而使 Node.js 进程继续。

调用监听器回调函数时将 process.exitCode 的值作为唯一的参数传入。

对于导致显式终止的条件，例如调用 process.exit() 或未捕获的异常，则不会触发 'beforeExit' 事件。

'beforeExit' 不应用作 'exit' 事件的替代，除非打算安排额外的工作。

import process from 'process';

process.on('beforeExit', (code) => {
  console.log('Process beforeExit event with code: ', code);
});

process.on('exit', (code) => {
  console.log('Process exit event with code: ', code);
});

console.log('This message is displayed first.');

// 打印:
// This message is displayed first.
// Process beforeExit event with code: 0
// Process exit event with code: 0
```

```
'exit' 事件#
中英对照

新增于: v0.1.7
code <integer>
当 Node.js 进程由于以下任一原因即将退出时，则会触发 'exit' 事件：

process.exit() 方法被显式调用；
Node.js 事件循环不再需要执行任何额外的工作。
此时没有办法阻止事件循环的退出，一旦所有 'exit' 监听器都运行完毕，则 Node.js 进程将终止。

监听器回调函数使用 process.exitCode 属性指定的退出码或传给 process.exit() 方法的 exitCode 参数调用。

import process from 'process';

process.on('exit', (code) => {
  console.log(`About to exit with code: ${code}`);
});
监听器函数必须只执行同步的操作。 Node.js 进程将在调用 'exit' 事件监听器之后立即退出，从而使任何仍在事件循环中排队的其他工作被丢弃。 例如，在以下示例中，超时永远不会发生：

import process from 'process';

process.on('exit', (code) => {
  setTimeout(() => {
    console.log('This will not run');
  }, 0);
});
```
```
- SIGINT       P1990      Term    Interrupt from keyboard
- https://man7.org/linux/man-pages/man7/signal.7.html

信号事件#
中英对照

当 Node.js 进程收到信号时，则将触发信号事件。 有关标准 POSIX 信号名称（例如 'SIGINT'、'SIGHUP' 等）的列表，请参阅 signal(7)。

信号在 Worker 线程上不可用。

信号句柄将接收信号的名称（'SIGINT'、'SIGTERM' 等）作为第一个参数。

每个事件的名称将是信号的大写通用名称（例如 'SIGINT' 表示 SIGINT 信号）。

import process from 'process';

// 从标准输入开始读取，因此进程不会退出。
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('Received SIGINT. Press Control-D to exit.');
});

// 使用单个函数处理多个信号
function handle(signal) {
  console.log(`Received ${signal}`);
}

process.on('SIGINT', handle);
process.on('SIGTERM', handle);
'SIGUSR1' 由 Node.js 预留以启动调试器。 可以安装监听器，但这样做可能会干扰调试器。
'SIGTERM' 和 'SIGINT' 在非 Windows 平台上具有默认的句柄，其在使用代码 128 + signal number 退出之前重置终端模式。 如果这些信号之一安装了监听器，则其默认行为将被删除（Node.js 将不再退出）。
'SIGPIPE' 默认情况下忽略。 它可以安装监听器。
'SIGHUP' 在 Windows 上是在关闭控制台窗口时生成，在其他平台上是在各种类似条件下生成。 参见 signal(7)。 它可以安装监听器，但是 Node.js 将在大约 10 秒后被 Windows 无条件地终止。 在非 Windows 平台上，SIGHUP 的默认行为是终止 Node.js，但一旦安装了监听器，则其默认行为将被删除。
'SIGTERM' Windows 上不支持，可以监听。
所有平台都支持来自终端的 'SIGINT'，通常可以使用 Ctrl+C 生成（但是这是可配置的）。 当启用终端原始模式并使用 Ctrl+C 时不会生成它。
'SIGBREAK' 在 Windows 上，当按下 Ctrl+Break 时会发送。 在非 Windows 平台上，它可以被监听，但无法发送或生成它。
'SIGWINCH' 当调整控制台大小时会发送。 在 Windows 上，这只会发生在当光标移动时写入控制台，或者当在原始模式下使用可读的终端时。
'SIGKILL' 不能安装监听器，它会无条件地终止所有平台上的 Node.js。
'SIGSTOP' 不能安装监听器。
'SIGBUS'、'SIGFPE'、'SIGSEGV' 和 'SIGILL'，当没有使用 kill(2) 人为引发时，本质上会使进程处于调用 JS 监听器不安全的状态。 这样做可能会导致进程停止响应。
0 可以发送来测试进程是否存在，如果进程存在则没影响，如果进程不存在则抛出错误。
Windows 不支持信号，因此没有等价的使用信号来终止，但 Node.js 提供了一些对 process.kill() 和 subprocess.kill() 的模拟：

发送 SIGINT、SIGTERM、和 SIGKILL 会导致目标进程无条件的终止，之后子进程会报告进程被信号终止。
发送信号 0 可以作为独立于平台的方式来测试进程是否存在。


```


## recommend
- https://zhuanlan.zhihu.com/p/101917567 - 语雀

### chalk
- https://www.npmjs.com/package/chalk
- 调试时候可以用，这样比较显眼

### 网关
- https://mp.weixin.qq.com/s/nWKCX1INkP7uKGONzW7CPg
- 大规模 Node.js 网关的架构设计与工程实践

### 服务间接口调用
- consul 测试环境 ip+端口号
- cluster IP + 80 线上环境
- 没有用域名做代理，当然会存在cluster ip更换的问题，不过相对稳定
- 

### windows 
系统属性里面的环境变量设置

## node - test框架推荐
- ava这个框架

## preventing-sql-injection-in-node-js
- https://stackoverflow.com/questions/15778572/preventing-sql-injection-in-node-js
- https://github.com/mysqljs/mysql#escaping-query-values


## problems - BFF


## cases
### BFF
- Java服务提供数据 - RPC通信
- 模版渲染
- API服务 - restful（易读，快速启动，数据聚合劣势）- github的v3 API的实现
- API服务 - GraphQL（专注数据聚合，返回前端需要的）

### config
- https://github.com/node-config/node-config
- https://www.npmjs.com/package/yaml
- package.json - config - process.env.npm_package_config_port - npm config set aaa:xxx 80


### 钩子
- 在node_modules/.hooks/{eventname}中放置一个可执行文件，所有根目录下的package.json文件在运行到该生命周期节点时都会被执行
- husky

### 端口冲突问题
- lsof -i:3000 | xargs killall
- npm i -g kp  -  kp 3000

### node-demo
- https://github.com/hua1995116/node-demo
```
node文件上传详解
node-rpc调用详解
跨域 demo
重拾css[一]伪元素、包含块和高度坍塌
React Hooks中这样写HTTP请求可以避免内存泄漏
```

### node-jiti
"Node-jiti"是一个Node.js库，可在运行时（JIT）转译并加载ECMAScript模块。以下是使用"node-jiti"的一些最佳实践：

1. **选择正确的环境**：“node-jiti”是一个在Node.js环境中运行的库，因此你应该确保你的项目是在Node.js环境中运行的。

2. **使用包管理器**： 使用npm或者yarn这种包管理器来安装和管理“node-jiti”，这样可以确保你总是使用最新、最稳定的版本。

3. **适当的错误处理**：“node-jiti”在加载或解析JS文件时可能会出现错误，因此应该适当地使用try...catch语句来处理可能采食的错误。

4. **理解ESM和CJS的区别**：“node-jiti”旨在使那些在运用时还不支持ESM的Node.js版本能够使用ESM，因此你需要对ESM和CJS两种模块系统有所了解。

5. **合理使用动态导入**：“node-jiti”允许你动态地导入JS文件，这是一种有用但需要谨慎使用的工具。因为过度使用动态导入可能会使代码难以理解和保持。

举例：简单的使用 `node-jiti` 加载一个模块：

```javascript
// 导入 node-jiti
const jiti = require('jiti')(__dirname)
// 使用 node-jiti 加载模块
const myModule = jiti('./myModule')
```

这是一个简单的示例，`jiti` 将加载并处理名为 `myModule.js` 的文件，此文件应该位于您的项目的根目录中。