---
title: dart使用感受
date: 2021-06-25 15:44:12
tags:
---

## overview

### 最好的了解网站-官网

- https://dart.cn/
- https://dart.cn/guides

> 讲，练，经验总结，风格指导为一体的官网，文档真的写的不错;

### 生态发展很快

- 官方全家桶提供，和两年前比起来，各方面生态迅速发展完备
- 国内可看闲鱼团队的一系列文章（https://juejin.cn/team/6932366495007801348/posts）

### 在线 repl

- https://dartpad.cn/
- https://replit.com/languages/dart

## Tips

### 通用概念
- 以main函数作为执行的入口
- 类型安全，所有类型都是对象类型（继承自顶层类型Object）
- 未初始化变量的值为null


### comparison with Javascript
#### if | assert ，dart中不能使用非布尔类型的值传入
### 特殊语法
- ```..```
```

``` 

## 深入语言

### baiscs
#### 基本的一些类型
- num (int | double) 都是64位，后者符合IEEE 754标准
- String UTF-16
- const 适用于定义编译常量
- final 适用于定义运行时常量