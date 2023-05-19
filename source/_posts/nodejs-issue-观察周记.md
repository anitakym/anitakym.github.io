---
title: nodejs-issue-观察周记
date: 2023-05-19 14:43:21
tags:
---
### 新运行时
1. Deno：
   - 由Node.js的创始人Ryan Dahl创建，致力于纠正Node.js中他认为的设计缺陷。
   - 采用V8引擎和Rust编程语言。
   - 内置TypeScript支持。
   - 提供类似Go语言的导入方式，允许从公共URL导入模块。
   - 遵循浏览器兼容的API。
   - 默认安全模式，需要明确授权才能访问文件系统，网络，环境变量等。
   - 支持WebAssembly。

2. Just：
   - 是一个轻量级的Node.js替代品。
   - 采用V8引擎和C++编写。
   - 面向内存优化、嵌入式编程和基于事件循环的高性能场景。
   - 包括少量内置模块和简化的核心API。
   - 支持Linux和macOS，但对Windows支持有限。
   - 非同步I/O，并专注于运行时性能。

3. Bun：
   - 由PolyFis创建，专注于高性能、小尺寸和安全性。
   - 采用V8引擎和C++编写。
   - 支持记号输出、优化跳过解析和单线程异步I/O。
   - 包括jsdom、WebSocket、HTTP/2等特性。
   - 支持WebAssembly。
   - 独特的内存分配和回收策略。
   - 支持Linux、macOS 和 Windows。
