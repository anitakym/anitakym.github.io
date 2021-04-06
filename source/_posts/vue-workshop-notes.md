---
title: vue-workshop-notes
date: 2021-04-03 17:00:15
tags:
---
> 以前听的Evan You的一个workshop的笔记

### Reactivity 
- imperative/declarative
  <pre>
  命令式和声明式
  我们先把命令式的行为转为声明式的，可以通过函数（声明关系），再进一步抽象，抽象成模版语言
  view = render(state)是视图渲染系统都用的高度抽象的模式
  我们不允许用户任意操控状态，而是让他们总是来调用一个函数来操控状态
  对于这个函数，react中就是setState, 但是在Vue和Angualr中，我们不需要调用setState，angularJS用dirty checking实现（比较旧的版本了），拦截实践，然后执行一个digest cyle, 就不管有没有变化，都会检查；但是Vue要做得更精细一点，会把state 对象变成响应式的
  用ES5 的 object.defineProperty API来将所有property都变成getters and setters
  刚刚的方法，其实是一个很基本的依赖追踪的形式，knockout.js,meteor tracker,vue,mobx中都是这样的
  </pre>

- getters and setters
  <pre>
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
  </pre>