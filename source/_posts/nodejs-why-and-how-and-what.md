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
- event loop
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop
- https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#what-is-the-event-loop
- 理解调用栈
(理解好浏览器和node环境的差异，为什么需要eventloop，为什么node端的是更精细化的设计)
- browser (https://github.com/luokuning/blogs/issues/1 - Object.observe为什么要被移除)
### Promise
#### What
- 当前事件循环得不到的结果，未来的事件循环会给到结果
- 状态机 - pending => fulfilled/resolved | rejected
- .then | .catch
- rejected状态后无.catch的Promise，会造成browser｜node环境的全局错误
- 执行then，catch之后会返回一个新的Promise，该Promise的最终状态根据回调函数的执行结果决定
- 回调函数：throw -> Promise状态是： rejected | return -> resolved
- 如果回调函数return了一个Promise，这个Promise会和回调函数return的Promise状态保持一致
- Promise.all  并发异步，catch拿第一个error的
### async/await
- async function 是 Promise的语法糖封装(console出来可以验证)
- 以同步的方式写异步-异步编程终极方案
- 以同步的写法获取Promise的执行结果            
- try-catch可以获取await得到的错误
- Event Loop -> 逻辑思维上的转变
- 并行异步任务 -> +Promise.all

### http
- http服务 -> 解析请求报文 && 返回对应的返回报文
- IncomingMessage - Class - doc
#### Express
Express - http服务框架
- 核心功能 && 解决的问题 -> what - 路由&&(req&&res简化)&&middleware | why
- middleware - 组织流程代码 ｜ 异步会打破express的洋葱模型
- https://www.npmjs.com/package/express
#### Koa
- (req&&res简化) - 更简单明了
- async - 在异步情况下，也符合洋葱模型
- 精简内核，额外功能都移到了middleware实现

### RPC
- Remote Procedure Call
#### 和Ajax的比较-相同
- 两端的网络通信
- 需要约定数据格式

#### 和Ajax的比较-差异
- 不一定使用DNS作为寻址服务
- 应用层协议一般不使用HTTP
- 基于TCP或者UDP协议

#### RPC调用
- 寻址｜负载均衡
 - Ajax使用DNS进行寻址
 - RPC使用特有服务进行寻址
- TCP通信方式
 - 单工通信
 - 半双工通信
 - 全双工通信
- 二进制协议
 - 更小的数据包体积
 - 更快的编解码速率

- https://github.com/tars-node 
- https://github.com/tars-node/rpc

### Buffer编解码二进制数据包
#### 大小端问题 
- 几个Byte里，高位与低位的编排顺序不同
#### 处理方法与String接近
- 使用concat 而不是 + ，避免utf-8字符拼接问题
#### Protocol Buffer
- Google研发的二进制协议编解码库
- 通过协议文件控制Buffer的格式 - 直观｜好维护｜方便协作

### net 搭建多路复用的RPC通道
- 单工｜半双工的通信通道搭建
- 全双工的通信通道搭建
 - 应用层协议需要有标记包号的字段
 - 需要有标记包长的字段（粘包，不完整包）
 - 错误处理
- netty - java的rpc通信
## source code
#### 内置模块
- os.js - internalBinding - node_os.cc - libuv
- v8
- 




## basic
### globals
#### process
-  A swiss army knife global. An Object that contains all the context you need about the current program being executed. Things from env vars, to what machine you're on.
```
当 Node.js 进程收到信号时，则将触发信号事件。 
Linux supports the standard signals listed below.  The second
       column of the table indicates which standard (if any) specified
       the signal: "P1990" indicates that the signal is described in the
       original POSIX.1-1990 standard; "P2001" indicates that the signal
       was added in SUSv2 and POSIX.1-2001.
       
process.on('SIGINT', () => {
  console.log('Received SIGINT. Press Control-D to exit.');
});

```
- https://man7.org/linux/man-pages/man7/signal.7.html -   SIGINT-P1990-Term-Interrupt from keyboard

```
Windows 不支持信号，因此没有等价的使用信号来终止，但 Node.js 提供了一些对 process.kill() 和 subprocess.kill() 的模拟：

发送 SIGINT、SIGTERM、和 SIGKILL 会导致目标进程无条件的终止，之后子进程会报告进程被信号终止。
发送信号 0 可以作为独立于平台的方式来测试进程是否存在。
```










## 其他语言
### golang
- coroutines
### erlang
- 抢占式调度



## performance
#### http服务性能测试
- 优化性能的前提 - 性能检查
- 压测工具 - ab|webbench
- 服务器性能指标 - QPS｜吞吐量
- 找到性能瓶颈 - top|iostat

#### nodejs性能分析工具
- nodejs - profile
- chrome devtool
- npm - clinic

#### js代码性能优化
- 根据性能分析结果优化
- 准则
  - 减少不必要的计算 - 提前计算（启动阶段？服务阶段）
  - 空间换时间？

#### 内存优化管理
- 垃圾回收
```
新生代 - 容量小，垃圾回收更快
老生代 - 容量大，垃圾回收更慢
减少内存使用，是提高服务性能的手段
内存泄漏会导致服务性能问题
```
- nodejs buffer 的内存分配策略
- 节省内存的最好方式是 - 使用池

#### C++插件
- 编译环境
  - node-gyp(node-gyp本身，对应的node版本编译环境)
  - python
- 将计算量转移到C++进行
  - 收益：C++运算比JS更快的部分｜成本：C++变量和V8变量的转换

#### nodejs子进程与线程
- 进程（操作系统挂载运行程序的单元｜拥有一些独立的资源，如内存等）
- 线程（进行运算调度的单元｜进程内的线程共享进程内的资源）
- nodejs的事件循环
```
- 主进程运行v8与Javascript
- 多个子线程通过时间循环被调度
```
- 使用子进程或者线程利用更多的CPU资源

#### cluster
- 主进程启动多个子进程，由主进程轮流分发请求，子进程代为处理

#### 进程守护
- nodejs的稳定性
- 防止僵尸进程（心跳）
- 死亡重启
- 数据监控

### 动静分离
- 静态内容-基本不会变动，也不会因为请求参数不同而变化 -> CDN分发，http缓存
- 动态内容-各种因为请求参数不同而变动，且变种的数量几乎不可枚举 -> 加机器，结合反响代理进行负载均衡
## Tools
#### volta - The Hassle-Free JavaScript Tool Manager
- https://volta.sh/

## 框架设计和工程化 
> 软件质量体系，https://juejin.cn/post/6990365231348187150 - 设计模式经典书籍
- 架构设计 （底层更稳固->程序不容易崩溃，容易往上搭-扩展新功能更方便）
- 工程工具（更加易于施工-学习上手成本低，保证施工安全-不会因为操作失误搞挂程序）

- 给工程师使用的产品
  - 开发体验（可维护性，可靠性，易用性）
  - KISS（Vue渐进式）

### 设计模式
- 模式只是达到目的的手段
- PD这本书-1995-基于Java语言本身的一些特性-elements of reusable object-oriented software
#### 观察者模式
- EventEmitter（node-process）
- DOM addEventListener
```
在 Node.js 中，EventEmitter 是一个用于处理事件的模块。它提供了一种基于观察者模式的异步编程方式，可以在需要时触发事件和处理事件。以下是一些使用 EventEmitter 的常见场景：

数据库连接：当使用 Node.js 连接到数据库时，可以使用 EventEmitter 来处理成功或失败的情况，并确保连接正确关闭。

网络编程：在编写网络应用程序时，使用 EventEmitter 可以轻松地管理套接字和客户端连接，并处理相关的事件，例如数据传输、断开连接等。

文件系统：Node.js 的文件系统模块也使用 EventEmitter 来通知进程有关文件操作的事件（如读取、写入、删除等）。

自定义事件：通过继承 EventEmitter 类并添加自己的方法和属性，可以创建自己的类，并发出自定义事件来实现各种功能。

总之，EventEmitter 在 Node.js 中非常常用，几乎在任何需要处理异步事件的场景中都可能会用到。无论是处理数据库连接、网络编程还是文件系统操作，使用 EventEmitter 都可以帮助我们轻松地管理异步事件，保持代码的模块化和可读性。

观察者模式是一种设计模式，用于处理对象间的一对多依赖关系，并在对象状态发生变化时自动通知所有依赖项。在观察者模式中，被观察的对象称作主题（Subject），而观察它的对象称为观察者（Observer）。

观察者模式的主要思想是，当主题对象状态发生变化时，它会通知所有已注册的观察者对象，并调用它们的更新方法来执行相应的操作。这使得主题和观察者可以解耦，避免了紧密耦合的代码结构，也提高了系统的可扩展性和可维护性。

观察者模式通常包括以下角色：

主题（Subject）：被观察的对象，它包含了观察者需要监视的状态以及注册和删除观察者的方法。

观察者（Observer）：观察主题对象的状态，并在状态发生变化时执行相应的操作。

具体主题（Concrete Subject）：具体的被观察对象，它维护了一个观察者列表，并且负责通知所有已注册的观察者。

具体观察者（Concrete Observer）：具体的观察者对象，实现了更新方法，并定义了在主题状态发生变化时所执行的操作。

观察者模式可以应用于许多场景，例如GUI事件处理、文档自动保存、股票市场监控等。它可以帮助我们实现松耦合的代码结构，并提高系统的可扩展性和可维护性。

RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using Observables to handle asynchronous and event-based workflows in JavaScript. It provides operators for transforming, filtering, combining, and querying data streams, as well as utilities for managing subscriptions and handling errors. RxJS is commonly used in front-end web development with frameworks such as Angular or React.
RxJS 的使用场景主要是处理复杂的异步和事件驱动场景，例如：

处理 HTTP 请求：RxJS 的 Observable 类型可以方便地处理 HTTP 请求和响应，并使用操作符进行数据转换、筛选和组合。

处理用户界面输入：RxJS 可以处理用户界面上的各种事件（如点击、滚动、输入等），并将它们转换成 Observable 流，使得开发者可以方便地编写响应式代码。

处理 WebSocket 数据流：RxJS 可以轻松处理 WebSocket 数据流，并基于数据流执行各种操作，例如过滤、聚合、映射等。

处理复杂的状态管理：RxJS 可以用于处理复杂的状态管理场景，例如 Redux 和 NgRx 中的数据流管理和副作用管理。

处理数据可视化：RxJS 可以用于实现数据可视化和动画效果，例如基于数据流控制图表的更新和动画过渡效果。

总之，RxJS 主要适用于需要处理异步和事件驱动场景的项目，尤其是在需要对数据进行转换、组合和筛选时。

```

#### 外观模式
- jQuery（解决兼容性问题）
```
elem.on('', func)
if else - 各种浏览器
```

#### 6原则
- 单一职责 (微服务) - 每一个模块都有明确的功能
- 开闭原则 - 对扩展开放，对修改关闭 - css-loader ts-loader| webpack - 新增功能只需要增加模块，不需要修改原有部分
。。。like lego

