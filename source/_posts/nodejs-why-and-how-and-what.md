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
- 当前事件循环得不到的结果，未来的事件循环会给到结果
- 状态机 - pending | fulfilled/resolved | rejected
- .then | .catch
- rejected状态后无.catch的Promise，会造成browser｜node环境的全局错误
- 回调函数的执行结果 - throw｜ return -> rejected | resolved
### async/await
- async function 是 Promise的语法糖封装
- 以同步的方式写异步
- try-catch可以获取await得到的错误
- Event Loop -> 逻辑思维上的转变

### http
- http服务 -> 解析请求报文 && 返回对应的返回报文
#### Express
Express - http服务框架
- 核心功能 && 解决的问题 -> what - 路由&&(req&&res简化)&&middleware | why
- middleware - 组织流程代码 ｜ 异步会打破express的洋葱模型
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
 - 更小的数据包提及
 - 更快的编解码速率

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
## source code
#### 内置模块
- os.js - internalBinding - node_os.cc - libuv
- v8
- 




## basic

#### process
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


## Tools
#### volta - The Hassle-Free JavaScript Tool Manager
- https://volta.sh/
