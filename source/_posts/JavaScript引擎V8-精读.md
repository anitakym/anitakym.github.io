---
title: JavaScript引擎V8-精读
date: 2021-04-30 22:45:33
tags:
---
- https://v8.dev/docs
为什么要？
知其然知其所以然，对知识本身的理解，越往后走，走过的前面的内容就越简单

工作中，一些性能调优，问题解决负责团队的项目涉及(browser,node,electron)


#### github
- https://github.com/v8/v8.git

需要比较长解释的，就单独新一个链接
#### Event-Loop事件循环
- 异步
#### 垃圾回收


https://v8.dev/blog/math-random

### 率先引入
- V8之前，JS的虚拟机都是解释执行，V8率先引入JIT的双轮驱动设计 - 权衡策略 （混合编译执行和解释执行两种手段）
- 惰性编译（加速代码启动速度）、内联缓存、隐藏类（Hide Class，将动态类型转换为静态类型，消除动态类型语言执行速度过慢点问题）
### V8的编译流水线

### others
- Any application that can be written in JavaScript, will eventually be written in JavaScript. - Jeff Atwood
- The strength of JavaScript is that you can do anything. The weakness is that you will. - Reg Braithwaite