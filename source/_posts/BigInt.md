---
title: BigInt
date: 2021-03-16 17:48:15
tags:
---
### 文档指南：
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


### 类型转换
```
“等值（==）”运算中，不能确定左、右操作数的类型；（JavaScript 认为，如果左、右操作数之一为 string、number、bigint 和 symbol 四种基础类型之一，而另一个操作数是对象类型 (x)，那么就需要将对象类型“转换成基础类型（ToPrimitive(x)）”来进行比较。操作数将尽量转换为数字来进行比较，即最终结果将等效于：Number(x) == Number(y)。）
```

### 相关
- V8——2018 年，团队为 WebAssembly 发布了一个名为 Liftoff 的基线编译器，它大大减少了 WebAssembly 应用程序的启动时间，同时提供了可预测的性能。并且发布了 BigInt，这是一个新的 JavaScript 原始类型，可以实现任意精度的整数。