---
title: OC-summary
date: 2023-04-17 18:05:24
tags:
---
### 介面与实现 - 编写
#### 类的介面 - interface
- 只有声明，没有实现
- 可以声明：属性，变量，方法

#### 类的实现 - implementation
- 需要实现介面声明的方法
- 可添加介面没有的：变量，方法（私有）

- 在 TypeScript 中，类定义是使用关键字 class 来声明的，而不是 Objective-C 中的 @interface 或 @implementation。

#### .h
- 可被.h/.m引入
- @interface可写在.h/.m
#### .m
- 不可被引入
- @implementation可写在.m

### 对象与构造函数
- 创建对象
- override父类的构造函数
- 声明，实现带参数的构造函数

### 函数方法
- 声明
- 实现
- 方法调用 - 实例方法，静态方法

### 成员变量
- interface变量
- implementation 变量
- 外部透过对象访问公开成员变量
- 内部可以访问公开和私有成员变量

### 访问变量
- 公开Get/Set方法
- _私有变量

### @property属性
- 属性特性

### 协议 @protocol
- 语法

### 动态增删改方法 -> runtime, oc黑魔法