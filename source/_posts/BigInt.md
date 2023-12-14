---
title: BigInt
date: 2021-03-16 17:48:15
tags:
---
### 文档指南：
https://v8.dev/features/bigint
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt

TC39——（18年fullstack大会上，Brendan Eich介绍，会在TC39加入BigInt：这是一种新的值类型，用于处理任意精度的整数；）
https://tc39.es/ecma262/#sec-bigint-objects
```
21.2.1 The BigInt Constructor
The BigInt constructor:

is %BigInt%.
is the initial value of the "BigInt" property of the global object.
performs a type conversion when called as a function rather than as a constructor.
is not intended to be used with the new operator or to be subclassed. It may be used as the value of an extends clause of a class definition but a super call to the BigInt constructor will cause an exception.
```

### 查看浏览器是否实现了这个API
```
let target = new Set()
let arrs = ["BigInt"]
arrs.forEach(o=>target.add(o))
let all = Object.getOwnPropertyNames(window)
let ifHas = all.filter(e=>target.has(e))
```

### 最大安全数
https://2ality.com/2013/10/safe-integers.html


### 延伸
String的maxLength
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length
```
This property returns the number of code units in the string. UTF-16, the string format used by JavaScript, uses a single 16-bit code unit to represent the most common characters, but needs to use two code units for less commonly-used characters, so it's possible for the value returned by length to not match the actual number of characters in the string.

ECMAScript 2016 (ed. 7) established a maximum length of 2^53 - 1 elements. Previously, no maximum length was specified. In Firefox, strings have a maximum length of 2**30 - 2 (~1GB). In versions prior to Firefox 65, the maximum length was 2**28 - 1 (~256MB).

For an empty string, length is 0.

The static property String.length is unrelated to the length of strings, it's the arity of the String function (loosely, the number of formal parameters it has), which is 1.
```

### 类型转换
```
“等值（==）”运算中，不能确定左、右操作数的类型；（JavaScript 认为，如果左、右操作数之一为 string、number、bigint 和 symbol 四种基础类型之一，而另一个操作数是对象类型 (x)，那么就需要将对象类型“转换成基础类型（ToPrimitive(x)）”来进行比较。操作数将尽量转换为数字来进行比较，即最终结果将等效于：Number(x) == Number(y)。）
```

### 相关
- V8——2018 年，团队为 WebAssembly 发布了一个名为 Liftoff 的基线编译器，它大大减少了 WebAssembly 应用程序的启动时间，同时提供了可预测的性能。并且发布了 BigInt，这是一个新的 JavaScript 原始类型，可以实现任意精度的整数。

### A small, fast JavaScript library for arbitrary-precision decimal arithmetic.
- https://github.com/MikeMcl/big.js/
```
一个小型、快速的 JavaScript 库，用于任意精度的十进制运算。
简单的应用程序接口
比 JavaScript 版本的 Java BigDecimal 更快、更小、更易用
最小化后仅 6 KB
复制 JavaScript Numbers 的 toExponential、toFixed 和 toPrecision 方法
以可访问的十进制浮点格式存储数值
全面的文档和测试集
无依赖关系
仅使用 ECMAScript 3，因此可在所有浏览器中运行
是 bignumber.js 和 decimal.js 的姊妹篇。关于它们之间的区别，请参阅此处。
```

### mathjs
- https://github.com/josdejong/mathjs
- Math.js 是一个适用于 JavaScript 和 Node.js 的广泛数学库。它具有灵活的表达式解析器，支持符号计算，提供了大量内置函数和常量，并提供了处理不同数据类型（如数字、大数、复数、分数、单位和矩阵）的集成解决方案。功能强大，易于使用。