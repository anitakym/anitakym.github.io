---
title: Android-ART-notes
date: 2023-01-11 17:39:21
tags:
---
## history
Dalvik
- 使用解释  JIT

ART(4.4Kitkat-5.0Lollipop) Android RunTime
- gc优化
- AOT(Ahead-of-time)

ART（7.0Nougat）
- 三种执行方式并存，引入speed profile

### overview
- compiler&interpreter
  - 解释器
  - JIT
  - AOT
- runtime
  - 内存管理
  - 类管理
  - intrinsic
  - 异常
  - String
  - 调试
  - 线程
  - JNI
  - monitor

## 对象
### 对象如何分配出来的
who = 类的管理
from where = 内存分配
to where = 内存回收

### 对象lifecycle
- 对象分配
- 对象使用
- 对象销毁
## 执行
### 虚拟机为了保证代码执行提供的机制
虚拟机的执行方式
开始和结束 = 栈管理
高效的执行 = 多线程
