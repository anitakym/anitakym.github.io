---
title: perf
date: 2021-06-11 16:33:58
tags:
---
node的项目

监控 && 压测
客户端监控
监控和日志，找出问题共性

性能问题排查：
cpu 负载 —— top
java 的话，jstack 查看CPU使用率比较高的线程正在执行什么操作
pidstat,vmstat,mpstat查看CPU的运行队列，阻塞进程数，上下文切换的数量
perf 排查哪些系统调用or操作消耗了更多的CPU时间
jmap dump 出内存信息，使用类似MAT工具来分析，排查内存泄漏问题
pmap ,GDB 查看堆外内存都有哪些数据，排查堆外内存泄漏的问题

perf 对系统内核线程进行分析时，内核线程依然还在正常运行中，所以这种方法也被称为动态追踪技术。

动态追踪技术，通过探针机制，来采集内核或者应用程序的运行信息，从而可以不用修改内核和应用程序的代码，就获得丰富的信息，帮你分析、定位想要排查的问题。

perf 简单的静态跟踪机制; 可以通过 perf ，来自定义动态事件（perf probe），只关注真正感兴趣的事件

Molnar

https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/tools/perf

centos
yum install perf

perf top 可以实时查看当前系统进程函数占用率情况

### debug
```
python id

获取的都不是真实内存


id(object)
Return the “identity” of an object. This is an integer which is guaranteed to be unique and constant for this object during its lifetime. Two objects with non-overlapping lifetimes may have the same id() value.
CPython implementation detail: This is the address of the object in memory.
Raises an auditing event builtins.id with argument id.
```
https://medium.com/fhinkel/debug-v8-in-node-js-core-with-gdb-cc753f1f32


js取不到的，用chrome的heap snapshot，能看到一个等价的地址，但不是真实的内存地址

js不提供对内存的直接访问，debug工具也只提供到vm的虚拟内存空间，想要取到底层的进程虚拟内存空间，只有用gdb去调试引擎源代码

https://www.v2ex.com/t/210556  -  JavaScript 堆内存分析新工具 OneHeap

https://v8.dev/docs

javascript heap snapshot

https://developers.google.com/web/tools/chrome-devtools/memory-problems/heap-snapshots