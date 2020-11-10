---
title: 表达式-语句-值-ES6-python
date: 2020-09-07 17:19:12
tags:
---

> 探究下不同语言中，表达式/语句是否有值的问题 ～ （问题来源于SICP(1.2.5)中对表达式和语句的阐述）

> 参考文档 —— SICP(1.2.5) + https://blog.csdn.net/aimingoo/article/details/51136511

SICP(1.2.5) —— In general, statements are not evaluated but executed; they do not produce a value but instead make some change.

比如在python当中：数字（以及表达式）自己在	Python	程序的上下文中会求解为值
 ```
 >>> x = 3
does not return a value nor evaluate a function on some arguments, since the purpose of assignment is instead to bind a name to a value.
 ```

但是在JS当中：
 ```
> a = 1
1
 ```
我们会看到如上输出
```
The value of a StatementList is the value of the last value producing item in the StatementList. For example, the following calls to the eval function all return the value 1:

The production IfStatement : if ( Expression ) Statement else Statement is evaluated as follows:

Let exprRef be the result of evaluating Expression.
If ToBoolean(GetValue(exprRef)) is true, then
a. Return the result of evaluating the first Statement.
Else,
eval("1;;;;;")
eval("1;{}")
eval("1;var a;")
```
具体对语句产生值的问题，可以看 https://blog.csdn.net/aimingoo/article/details/51136511 里面的阐释（说明了ES6中对这部分的处理）
