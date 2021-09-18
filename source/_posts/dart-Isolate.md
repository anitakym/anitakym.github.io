---
title: dart-Isolate
date: 2021-08-23 11:34:27
tags:
---

### 文档指南
- https://dart.dev/guides/language/language-tour#isolates
```
# 下面是文档里面给出的深入阅读链接，基本上看完对原理和应用场景就比较清晰了
Dart asynchronous programming: Isolates and event loops
(https://medium.com/dartlang/dart-asynchronous-programming-isolates-and-event-loops-bffc3e296a6a)
dart:isolate API reference, including Isolate.spawn() and TransferableTypedData
(https://api.dart.dev/stable/2.14.2/dart-isolate/dart-isolate-library.html)
Background parsing cookbook on the Flutter site
(https://flutter.dev/docs/cookbook/networking/background-parsing)
Isolate sample app
(https://github.com/flutter/samples/tree/master/isolate_example)
```


### 概述
DART：
- 基于“单线程”的
- 提供了 Isolate 这样的“多线程”能力
- 并发 Isolate 处理 CPU 密集型任务
- 基于消息机制通知主 Isolate 运行结果

### 使用场景
- compute函数