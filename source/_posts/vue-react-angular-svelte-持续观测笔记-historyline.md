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
```
$scope是个树形结构 
看源代码——debug 此bootstrap非彼bootstrap
启动～ angular.js 用自执行函数的形式让整个代码在加载完成后立即执行 window.angular
angular.injector angular.module
自启动（ng-app），手动启动 angular.element(document) angular.element = jqLite
window.angular.bootstrap(是否多次启动)
bindjQuery();(jqlite)
发布ng提供的API publishExternalAPI() extend() setupModuleLoader(window)——建立模块机制 注册内核provider
angularInit()——防止多次初始化ng-app, bootstrap——创建injector、拉起内核和启动模块，调用compile服务
推断型注入（混淆之后名称都会改，就没有办法了） 声明式注
内联式注入（推荐）
创建注射器（provider，instance） $injector.invoke() $injector.annotate()——分析函数参数的 function 的 toString();
核心目的：让接口和实现分离 在ng中，所有的provider都可以用来进行注入
provider/factory/service/constant/value provider是基础，其余都是调用provider函数实现的，只是参数不同 从坐向右，灵活性越来越差
return 语句可以放在前
```
- angular 2+ - 提供了样式封装能力，与组件深度集成
- shadowDOM- 逻辑上一个DOM，结构上存在子集结构
- scoped css - 随机属性
- this - 引用的是函数据以执行的环境对象，函数的名字仅仅是一个包含指针的变量
- toolbar generator - 根据type得到generator，generator实例化，调用generator的render方法

## Vue
### UI组件库
- https://github.com/didi/cube-ui - 移动端