---
title: node-ffi-napi
date: 2021-04-12 13:43:39
tags:
---
### 文档指南
https://github.com/node-ffi-napi/node-ffi-napi

### 历史进展
ffi
ffi-napi
1、这个项目太老了。NODE_MODULE_VERSION只支持到64,超过编译就报错，不管是node-gyp或者electron rebuild。
也就是说只要nodejs超过v12，则node-ffi编译就会报错，提示各种函数类型参数等不正确，只能node<v12来编译。。。
2、node：https://nodejs.org/zh-cn/download/releases/
electron:https://github.com/nodejs/node/blob/master/doc/abi_version_registry.json
大家伙可以看上边连接来对应两者的NODE_MODULE_VERSION,版本不相等则无法在electron调用node-ffi。
3、c模式的dll可以使用node-ffi，缺点nodejs不支持v12及以上，停更了。
4、c++模式的dll，有高人提供了ffi-napi且支持到nodejs v12.，但v12版本也很低(对应electron v5 现在稳定是v9)

### 概述
<pre>
Node.js Foreign Function Interface for N-API

node-ffi-napi is a Node.js addon for loading and calling dynamic libraries using pure JavaScript. It can be used to create bindings to native libraries without writing any C++ code.

node-ffi-napi是一个Node.js插件，用于使用JavaScript加载和调用动态库。它可以用来创建与本地库的绑定，而无需编写任何C++代码。

It also simplifies the augmentation of node.js with C code as it takes care of handling the translation of types across JavaScript and C, which can add reams(大量) of boilerplate code to your otherwise simple C. See the example/factorial for an example of this use case.
它还简化了用C代码的拓展node.js，因为它负责处理跨JavaScript和C的类型转换，这可能会给你原本简单的C语言增加大量的模板代码。

WARNING: node-ffi-napi assumes you know what you're doing. You can pretty easily create situations where you will segfault the interpreter and unless you've got C debugger skills, you probably won't know what's going on.
警告：除非get C debugger的技能，不然谨慎操作，因为很容易造成解释器崩溃的情况。

WARNING: The original API of node-ffi is left mostly untouched in the N-API wrapper. However, the API did not have very well-defined properties in the context of garbage collection and multi-threaded execution. It is recommended to avoid any multi-threading usage of this library if possible.

警告：在N-API包装器中，node-ffi的原始API大部分没有被触动。然而，在垃圾收集和多线程执行的情况下，该API并没有非常明确的属性。建议尽可能避免对该库进行任何多线程使用。

</pre>


### 名词解释
- A segmentation fault (aka segfault) is a common condition that causes programs to crash; they are often associated with a file named core . Segfaults are caused by a program trying to read or write an illegal memory location

- https://en.wikipedia.org/wiki/Segmentation_fault