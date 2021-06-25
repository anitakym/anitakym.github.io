---
title: nodejsWeb应用开发-精读
date: 2021-06-10 11:04:07
tags:
---
### Koa:
项目地址：
https://github.com/koajs/koa

一定要拉代码具体看，很适合看源码

### Koa-源码
#### Object.create() 
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create
```
// v1.x v2.x都使用了这种方式
const response = require('./response');
const context = require('./context');
const request = require('./request');
  this.context = Object.create(context);
  this.request = Object.create(request);
  this.response = Object.create(response);
```
- JavaScript高级程序设计（第4版）_ 原型式继承
```
// 警告 Object.setPrototypeOf()可能会严重影响代码性能。
// Mozilla文档说得很清楚：“在所有浏览器和JavaScript引擎中，修改继承关系的影响都是微妙且深远的。这种影响并不仅是执行Object.setPrototypeOf()语句那么简单，而是会涉及所有访问了那些修改过[[Prototype]]的对象的代码。”
// 为避免使用Object.setPrototypeOf()可能造成的性能下降，可以通过Object.create()来创建一个新对象，同时为其指定原型
let biped = {
  numLegs: 2
}
let person = Object.create(biped)
person.name = 'Matt'
console.log(person.name) // Matt
console.log(person.numLegs) // 2
console.log(person.getPrototypeOf(person) === biped) // true
// ECMAScript 5通过增加Object.create()方法将原型式继承的概念规范化了。这个方法接收两个参数：作为新对象原型的对象，以及给新对象定义额外属性的对象（第二个可选）。在只有一个参数时，Object.create()与这里的object()方法效果相同
// 原型式继承非常适合不需要单独创建构造函数，但仍然需要在对象间共享信息的场合。但要记住，属性中包含的引用值始终会在相关对象间共享，跟使用原型模式是一样的。
```

#### inspect
```
// util.inspect.custom support for node 6+
    /* istanbul ignore else */
    if (util.inspect.custom) {
      this[util.inspect.custom] = this.inspect;
    }
```

```
// 看下node源码 v16.3.0 lib/internal/util/inspect.js
/**
 * Echos the value of any input. Tries to print the value out
 * in the best way possible given the different types.
 *
 * @param {any} value The value to print out.
 * @param {Object} opts Optional options object that alters the output.
 */
/* Legacy: value, showHidden, depth, colors */
function inspect(value, opts) { ... }
inspect.custom = customInspectSymbol;

```