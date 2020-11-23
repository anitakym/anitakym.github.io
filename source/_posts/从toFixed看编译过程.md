---
title: 从toFixed看编译过程
date: 2020-11-16 13:34:29
tags:
---

MDN文档指路：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed
规范指路：https://tc39.es/ecma262/#sec-number.prototype.tofixed

The toFixed() method formats a number using fixed-point notation.

```
var numObj = 12345.6789;

numObj.toFixed();         // 返回 "12346"：进行四舍六入五看情况，不包括小数部分
numObj.toFixed(1);        // 返回 "12345.7"：进行四舍六入五看情况

numObj.toFixed(6);        // 返回 "12345.678900"：用0填充

(1.23e+20).toFixed(2);    // 返回 "123000000000000000000.00"

(1.23e-10).toFixed(2);    // 返回 "0.00"

2.34.toFixed(1);          // 返回 "2.3"

2.35.toFixed(1)           // 返回 '2.4'. Note it rounds up

2.55.toFixed(1)           // 返回 '2.5'. Note it rounds down - see warning above

-2.34.toFixed(1);         // 返回 -2.3 （由于操作符优先级，负数不会返回字符串）

(-2.34).toFixed(1);       // 返回 "-2.3" （若用括号提高优先级，则返回字符串）

1.toFixed();              // 返回VM81:1 Uncaught SyntaxError: Invalid or unexpected token

```
<pre>
Exceptions
RangeError
If digits is too small or too large. Values between 0 and 100, inclusive, will not cause a RangeError. Implementations are allowed to support larger and smaller values as chosen.
TypeError
If this method is invoked on an object that is not a Number.
</pre>

我们可以看到```1.toFixed();```报的是SyntaxError

```
1..toFixed()

let num = 1;
num.toFixed();

(1).toFixed();
```
改成上面三种形式皆可


V8如何处理toFixed的呢
