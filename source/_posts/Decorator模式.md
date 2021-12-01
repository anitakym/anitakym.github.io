---
title: Decorator模式
date: 2021-11-02 14:13:56
tags:
---
修饰器：


Object.assign()

基本用法
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。
注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。


Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

Object.defineProperty(obj, prop, descriptor)

obj
要在其上定义属性的对象。
prop
要定义或修改的属性的名称。
descriptor
将被定义或修改的属性描述符。


该方法允许精确添加或修改对象的属性。通过赋值操作添加的普通属性是可枚举的，能够在属性枚举期间呈现出来（for...in 或 Object.keys 方法）， 这些属性的值可以被改变，也可以被删除。这个方法允许修改默认的额外选项（或配置）。默认情况下，使用 Object.defineProperty() 添加的属性值是不可修改的。









为什么修饰器不能用于函数？
修饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。
var counter = 0;

var add = function () {
  counter++;
};

@add
function foo() {
}
上面的代码，意图是执行后counter等于 1，但是实际上结果是counter等于 0。因为函数提升，使得实际执行的代码是下面这样。
@add
function foo() {
}

var counter;
var add;

counter = 0;

add = function () {
  counter++;
};

函数声明提升

另一方面，如果一定要修饰函数，可以采用高阶函数的形式直接执行。
function doSomething(name) {
  console.log('Hello, ' + name);
}

function loggingDecorator(wrapped) {
  return function() {
    console.log('Starting');
    const result = wrapped.apply(this, arguments);
    console.log('Finished');
    return result;
  }
}

const wrapped = loggingDecorator(doSomething);
