---
title: nodejs来一打C++扩展-精读
date: 2021-05-13 01:57:05
tags:
---
> nodejs来一打C++扩展-死月


- Node.js 的模块机制
  - CommonJS 的模块规范
  - Node.js 的模块
- Node.js 的包机制
  - CommonJS 的包规范
  - Node.js / NPM 下的包
- NPM 与 CNPM(cnpm: npm client for China mirror of npm registry.npmmirror.com)
- Node.js 依赖
  - Chrome V8
  - libuv
  - 其他依赖
- C++ 扩展开发的准备工作
  - 编辑器 / IDE
  - node-gyp (https://github.com/nodejs/node-gyp#installation)
  - 其他构建工具
- C++ 模块原理简析
- 为什么要写 C++ 模块
  - C++ 比 JavaScript 解释器高效
  - 已有的 C++ 轮子
- 什么是 C++ 扩展
  - C++ 模块本质
  - Node.js 模块加载原理
- Chrome V8 基础
  - Node.js 与 Chrome V8
  - 基本概念(内存机制,隔离实例（Isolate）,上下文（Context）,脚本（Script）)
  - 句柄（Handle）(本地句柄（Local）持久句柄（Persistent）永生句柄（Eternal）待实本地句柄（Maybe Local）)
  - 句柄作用域(一般句柄作用域（Handle Scope）可逃句柄作用域（Escapable Handle Scope）)
  - 上下文（Context）
  - 模板（Template）
  - 函数模板（Function Template）
  - 对象模板（Object Template）
  - 对象模板的访问器（Accessor）与拦截器（Interceptor）
  - 对象模板的内置字段（Internal Field）
  - 函数模板的继承（Inherit）
  - 常用数据类型 
  - 基值（Value） 
  - 字符串（String）
  - 数值类型
  - 布尔类型（Boolean）
  - 对象（Object）
  - 函数(Function)
  - 数组（Array）
  - JSON 解析器
  - 函数回调信息（Function Callback Info）
  - 函数返回值（Return Value）
  - 隔离实例(Isolate)
  - 异常机制
  - try-catch
  - 抛出异常
  - 异常生成类（Exception）
- C++ 扩展实战初探
  - binding.gyp
  - 惊鸿一瞥
  - binding.gyp 基础结构
  - GYP 文件
  - 常用字段
  - 牛刀小试
  - 又是 Hello World
  - 函数参数
  - 回调函数
  - 函数返回
  - 循序渐进
  - C++ 与 JavaScript 类封装
  - 实例化 C++ 类封装对象的函数
  - 将 C++ 类封装对象传来传去
  - 进程退出钩子
- Node.js 原生抽象——NAN
  - Node.js 原生模块开发方式的变迁
    - 以不变应万变
    - 时代在召唤
  - 基础开发
    - 什么是 NAN
    - 安装和配置
    - 先睹为快——搭上NAN 的快车
    - 基础帮助函数和宏
    - 忽略 node_modules
  - JavaScript 函数
    - 函数参数类型
    - 函数声明
    - 函数设置
  - 常用帮助类与函数
    - 句柄相关
    - 创建数据对象
    - 与数据对象“玩耍”
    - 封装一个类
    - 异常处理
  - NAN 中的异步机制
    - Nan::AsyncQueueWorker
    - Nan::Callback
    - Nan::AsyncWorker
    - Nan::AsyncProgressWorker
- 异步之旅——libuv
  - 基础概念
    - 事件循环
    - 句柄（Handle）与请求（Request）
    - 尝尝甜头
  - libuv 的跨线程编程基础
    - libuv 的线程
    - 同步原语（Synchronization Primitive）
    - 工作队列
  - 跨线程通信
    - uv_async_t 句柄
    - Watchdog 半成品实战解析
    - Watchdog 试运行
- 实战——文件监视器
  - 准备工作
    - 功能规划
    - 文件系统监听库——efsw
  - 核心设计
    - API 设计
    - EFSWCore 的血肉之躯
    - EFSWCore 的灵魂
  - 编写JavaScript 类
    - 类的设计
    - 核心逻辑
    - 简单容错
  - 进一步完善
    - C++ 代码的完善
    - JavaScript 代码的完善
- 实战——现有包剖析
  - 字符串哈希模块——Bling Hashes
    - 文件设定
    - C++ 源码剖析
    - JavaScript 源码剖析
  - 类 Proxy 包——Auto Object
    - Proxy
    - Auto Object 使用范例
    - 代码剖析
- N-API——下一代 Node.js C++ 扩展开发方式
  - 浅尝辄止
    - 实现一个 Echo 函数
    - 尝试运行 N-API 扩展
    - 向下兼容
    - N-API Package——C++ 封装
  - 基本数据类型与错误处理
    - 基本数据类型
    - 与作用域及生命周期相关的数据类型
    - 回调数据类型
    - 错误处理
    - 模块注册
  - 对象与函数
    - 对象
    - 函数
    - 类的封装

.cc和.cpp都是C++源文件的扩展名，它们在功能上是没有区别的，都是用于存放C++编程代码。

这两种扩展名的使用主要取决于开发者的习惯或者团队的命名规范，以及所使用的编译器和开发环境。比如，GNU的C++编译器（g++）默认的源文件扩展名是.cc，而在很多Windows开发环境中，如Visual Studio，默认的扩展名是.cpp。

无论使用.cc还是.cpp，都不会影响源代码的编译和运行。一个比较好的实践就是在一个项目或者团队内部保持一致的命名规范，这样可以帮助提高代码的可读性和可维护性。

https://www.npmjs.com/package/node-addon-api

Node-addon-api和N-API是 Node.js 在尝试链接到C++代码时使用的工具集。

1. N-API：N-API是Node.js运行时提供的预构建的API，它能直接在JavaScript中调用，且无需重新编译，即使是在不同版本的Node.js上也可以使用。N-API的设计目标是消除在Node.js生态系统中的第三方扩展插件的维护负担和碎片化问题。通过这种方式，本地模块可以在不同版本和可能在未来的Node.js中无缝运行。

2. Node-addon-api：Node-addon-api是N-API的包装器，它是一个更高级别、更易于使用的API，其基于C++，提供了针对N-API的面向对象的抽象。 在大多数情况下，你会使用这个比N-API更高阶的 API, 因为它更易于构建和管理代码。

N-API的目标是提供稳定的Node API用于本地插件，而不受底层JavaScript运行时的改变影响，并且它对所有Node.js LTS版本提供支持。而Node-addon-api是为了简化C++版本的N-API的使用，提供了更友好和简洁的API。