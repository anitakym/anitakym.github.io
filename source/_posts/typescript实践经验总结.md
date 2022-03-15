---
title: typescript实践经验总结
date: 2021-03-08 12:07:02
tags:
---
> 多看下生成的JS，从而看看处理的逻辑（使用不同的ES标准进行编译）
### 几个迁移的案例
https://developers.google.com/web/updates/2021/01/puppeteer-typescript


### redaxios
https://www.tslang.cn/docs/handbook/type-checking-javascript-files.html
https://github.com/Microsoft/TypeScript/wiki/JSDoc-support-in-JavaScript
使用JSDoc注解
```
// https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html
支持的JSDoc
下面的列表列出了当前所支持的JSDoc注解，你可以用它们在JavaScript文件里添加类型信息。

注意，没有在下面列出的标记（例如@async）都是还不支持的。

@type
@param (or @arg or @argument)
@returns (or @return)
@typedef
@callback
@template
@class (or @constructor)
@this
@extends (or @augments)
@enum
它们代表的意义与usejsdoc.org上面给出的通常是一致的或者是它的超集。 
```

### 推荐相关文档：
https://zhuanlan.zhihu.com/p/40322215
https://labs.thisdot.co/blog/your-first-vue-3-app-using-typescript
https://medium.com/vue-typescript/vue-3-with-typescript-setup-a-new-project-with-the-vue-cli-4ea806be7a91


### 推荐TS入门：
https://basarat.gitbook.io/typescript/getting-started
https://jkchao.github.io/typescript-book-chinese/typings/types.html#%E4%BD%BF%E7%94%A8-types

### 教程推荐
- 英文OK的还是官方文档
    - https://www.typescriptlang.org/docs/handbook/basic-types.html
    - 更新及时，对应版本准确
- 中文的话：
    - http://ts.xcatliu.com/


## 项目总结

### 接入的第三方插件
#### sentry
- sentry本身就有@sentry/types，被JavaScript 相关的 SDK依赖，所以没啥问题，安装之后，就支持了
- https://getsentry.github.io/sentry-javascript/


### type vs interface
官方example
```
// There are two main tools to declare the shape of an
// object: interfaces and type aliases.
//
// They are very similar, and for the most common cases
// act the same.

type BirdType = {
  wings: 2;
};

interface BirdInterface {
  wings: 2;
}

const bird1: BirdType = { wings: 2 };
const bird2: BirdInterface = { wings: 2 };

// Because TypeScript is a structural type system,
// it's possible to intermix their use too.

const bird3: BirdInterface = bird1;

// They both support extending other interfaces and types.
// Type aliases do this via intersection types, while
// interfaces have a keyword.

type Owl = { nocturnal: true } & BirdType;
type Robin = { nocturnal: false } & BirdInterface;

interface Peacock extends BirdType {
  colourful: true;
  flies: false;
}
interface Chicken extends BirdInterface {
  colourful: false;
  flies: false;
}

let owl: Owl = { wings: 2, nocturnal: true };
let chicken: Chicken = { wings: 2, colourful: false, flies: false };

// That said, we recommend you use interfaces over type
// aliases. Specifically, because you will get better error
// messages. If you hover over the following errors, you can
// see how TypeScript can provide terser and more focused
// messages when working with interfaces like Chicken.

owl = chicken;
chicken = owl;

// One major difference between type aliases vs interfaces
// are that interfaces are open and type aliases are closed.
// This means you can extend an interface by declaring it
// a second time.

interface Kitten {
  purrs: boolean;
}

interface Kitten {
  colour: string;
}

// In the other case a type cannot be changed outside of
// its declaration.

type Puppy = {
  color: string;
};

type Puppy = {
  toys: number;
};

// Depending on your goals, this difference could be a
// positive or a negative. However for publicly exposed
// types, it's a better call to make them an interface.

// One of the best resources for seeing all of the edge
// cases around types vs interfaces, this stack overflow
// thread is a good place to start:

// https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/52682220#52682220

```

## Usage
- JavaScript - 动态弱类型 - 不会在变量的类型它们的调用者之间建立结构化的契约

- before ES标准（静态类型检查）,TS 是解决问题的最佳方案

- 静态类型检查器: Flow/Hegel（https://github.com/JSMonk/hegel）/Ternjs(2019停止更新-https://github.com/ternjs/tern)

### Class
#### constructor
- 见ES6的feature
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor
- 在类构造函数中，不能在调用super()之前引用this - cite  JavaScript高级程序设计（第四版）
- 如果在派生类中显式定义了构造函数，则要么必须在其中调用super()，要么必须在其中返回一个对象 - cite  JavaScript高级程序设计（第四版）
- Just as in JavaScript, if you have a base class, you’ll need to call super(); in your constructor body before using any this. members
```
constructor关键字用于在类定义块内部创建类的构造函数。
方法名constructor会告诉解释器在使用new操作符创建类的新实例时，应该调用这个函数。
构造函数的定义不是必需的，不定义构造函数相当于将构造函数定义为空函数。 
- cite  JavaScript高级程序设计（第四版）
```
#### TS 
- constructor
```
// 可以使用构造器来定义成员变量，即在类中拥有一个成员，并在构造器中初始化它
// 本写法采用了展开参数的形式，如果需要检查参数或者处理参数，则更合适
private start: number = 0
private end: number = 0
constructor(start: number, end: number) {
  this.start = start
  this.end = end
}

// typescript为上面的处理方法提供了一个简写
// 可以在成员中加一个修饰符前缀，它会在类上自动声明，并且从构造器中复制过去
// 写法简洁，适用于只是为私有字段赋值的场景；
constructor(private start: number, private end: number)


```
#### 把类当做接口使用
- 类定义会创建两个东西：类的实例类型和一个构造函数。 因为类可以创建出类型，所以你能够在允许使用接口的地方使用类。


> 很多JavaScript框架（特别是React）已经抛弃混入模式，转向了组合模式（把方法提取到独立的类和辅助对象中，然后把它们组合起来，但不使用继承）。这反映了那个众所周知的软件设计原则：“组合胜过继承（composition over inheritance）。”这个设计原则被很多人遵循，在代码设计中能提供极大的灵活性。 __ JavaScript高级程序设计（第四版）

### 联合类型
- type | type
- 确保使用typeof检查
- 如果类型过多，考虑设计上是否可以分解为更小的函数

### 交叉类型
- 可以让我们安全的使用extends 模式
- 适用于类，接口，泛型和基本类型

### 类型别名
- 语法技巧，提高代码可读性
- 大型项目，提高代码一致性
```
type Flags = PatchFlags | ShapeFlags
```
### ...
- 使用展开运算符，可以对一个或多个输入类型的属性自动执行浅拷贝
- 解构对象 - rest
- rest参数 ｜ rest属性

### 装饰器 && AOP

### Mixin

### 泛型
- 将相同的代码用于不同的类型
- String Stack, Number Stack ... ?
- TypeScript提供了创建泛型的能力
- 泛型是一种类型，通过占位符来代表要使用的类型
- 具体使用什么类型，要由调用该泛型的代码决定。泛型包含在< >内，出现在类名、方法名等的后面
- <T>语法告诉TypeScript，这个类中任何地方出现的T都指代传入的类型
- 当我们为泛型指定类型后，TypeScript会限制其不能改变

#### 泛型约束
- 

#### 映射
- 映射是一个泛型类，接受两种类型：为映射使用的键的类型，以及在映射中存储的对象的类型
- Map - get | set


#### declare
- https://www.typescriptlang.org/docs/handbook/declaration-files/by-example.html

## tsconfig
- strictNullCheck 建议设置true，如果有需要都允许的地方，可以使用联合类型