---
title: 深入理解typescript
date: 2021-05-25 17:51:09
tags:
---
### typescript 代码风格指南与代码约定

## Usage
- JavaScript - 动态弱类型 - 不会在变量的类型它们的调用者之间建立结构化的契约

- before ES标准（静态类型检查）,TS 是解决问题的最佳方案

- 静态类型检查器: Flow/Hegel（https://github.com/JSMonk/hegel）/Ternjs(2019停止更新-https://github.com/ternjs/tern)
#### 强类型语言
- Liskov,Zilles 1974 - 在强类型语言中，当一个对象从调用函数传递到被调用函数时，其类型必须与被调用函数中声明的类型兼容
- 强类型语言不允许改变变量的数据类型，除非进行强制类型抓换
- 不允许程序在发生错误后继续执行


#### 弱类型语言
- 变量可以被赋予不同的数据类型

#### 静态 ｜ 动态 类型语言
- 在什么阶段确定所有变了的类型
- 编译阶段 ｜ 执行阶段

#### typescript
- 拥有类型系统的JavaScript的超集
- 可以编译成pure JavaScript
- 类型检查｜语言扩展｜工具属性

#### advantage
- 接口定义代替文档
- IDE提效（开发）降本（维护）
- 类型思维

#### ts vs es6 数据类型
- common - Boolean｜Number｜String|Array|Function|Object|Symbol|undefined|null
- + void | any | never | 元祖 ｜ 枚举 ｜ 高级类型
#### 类型注解
- 相当于强类型语言中的类型声明
- （变量/函数）:type

#### 枚举
- 解决if else (可读性和可维护性差的问题)
- 一组有名字的常量集合
#### 类与接口
- interface （implements）class
- class (extends - public|private|protected) interface
- class（extends）class
- interface （extends）interface
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

#### 泛型
- 不预先确定的数据类型，具体的类型在使用的时候才能确定
- 将相同的代码用于不同的类型
- String Stack, Number Stack ... ?
- TypeScript提供了创建泛型的能力
- 泛型是一种类型，通过占位符来代表要使用的类型
- 具体使用什么类型，要由调用该泛型的代码决定。泛型包含在< >内，出现在类名、方法名等的后面
- <T>语法告诉TypeScript，这个类中任何地方出现的T都指代传入的类型
- 当我们为泛型指定类型后，TypeScript会限制其不能改变

#### 泛型优势
- 可扩展性-函数或类可以轻松支持多种数据类型
- 可读性 - 不用写多条函数重载｜冗长的联合类型声明
- 灵活控制类型之间的约束

#### 泛型约束

#### 类型检查机制
- TypeScript在做类型检查时，秉承的原则及表现出的行为
- 作用（提高开发效率）
- 类型推断（基础｜最佳通用｜上下文）
- 类型兼容性（当一个类型A可以被赋值给另一个类型B的时候，我们可以说B兼容A）（B兼容A： B = A ）（结构之间兼容-成员少的兼容成员多的；函数之间兼容-参数多的兼容参数少的）
- 类型保护（typescript能够在特定区块中保证变量属于某种确定的类型，可以在此区块中放心引用此类型的属性，或者调用此类型的方法）

### 映射
- 映射是一个泛型类，接受两种类型：为映射使用的键的类型，以及在映射中存储的对象的类型
- Map - get | set

## 工程
- typescript模块解析策略（classic｜node）
- awesome-typescirpt-loader(比ts-loader更适合与babel集成，使用babel的转义和缓存；不需要安装额外的插件，就可以把类型检查放在独立进程中进行）
#### babel
- babel7
- 之前和之后是两个处理路径
```
ts - tsc - js - babel - js
ts - babel - js (tsc - type checking)
```
#### 工具选择
- 1.tsc + ts-loader
- 2.babel + @babel/preset-typescript(可配合tsc做类型检查)
- 1.2不要混用

#### tslint vs eslint
- typescript官方转eslint
- why : 1.tslint执行规则的方式存在一些架构问题，从而影响了性能，而修复这些问题会破坏现有的规则 2.eslint的性能更好，并且社区用户通常有eslint的配置规则（Vue|react），没有tslint的规则
- typescript（类型检查｜语言转换｜语法错误）
- eslint(代码风格｜语法错误)

#### babel-eslint vs typescript-eslint
- 两者底层机制不一样，不要一起使用；babel体系使用babel-eslint,否则可以使用typescript-eslint
- babel-eslint支持typescript没有额外的语法检查，抛弃typescript，不支持类型检查
- typescript-eslint基于typescript的AST，支持创建基于类型信息的规则（tsconfig.json）

#### 工具体系
- 编译工具（ts-loader | @babel/preset-typescript）
- 代码检查工具（eslint+typescript-eslint | babel-eslint）
- 单元测试工具（ts-jest | babel-jest）