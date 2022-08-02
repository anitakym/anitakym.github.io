---
title: vue-react-angular-svelte-持续观测笔记-historyline
date: 2021-11-10 10:21:15
tags:
---

## angular
- angular.js(1.x) - 没有样式的集成能力
```
AngularJS中的服务其实就是提供一种方式抽取共用类库
创建服务的方式有三种：providers，factory，service
```
- angular 2+ - 提供了样式封装能力，与组件深度集成
- shadowDOM- 逻辑上一个DOM，结构上存在子集结构
- scoped css - 随机属性
- this - 引用的是函数据以执行的环境对象，函数的名字仅仅是一个包含指针的变量
- toolbar generator - 根据type得到generator，generator实例化，调用generator的render方法