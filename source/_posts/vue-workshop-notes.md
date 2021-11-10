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


  ## Words
  ## intro
- ins and outs 来龙去脉
- our agenda comprises of 议程包括
- resemble 类似
- under the hood 在底层
- field them with Vue.use, the API.
- And kind of walk you through how to use render functions in the Vue context 并指导你如何在Vue上下文中使用渲染函数

### reactivity
- is like streams and stuff 像流之类的东西
- when you change the state and how the state reflects in the update of the entire system.
- So this is a very naive imperative solution right? 所以这是一个很幼稚的命令式解决方案吧？
- procedural 程序性的
- the b1 cell is always kept in sync per(按照-in accordance with) the requirements of the spreadsheet
- So this internal representation, view = render(state) is the very high level abstraction of how all the view rendering systems work.
- So we'll not really bother with the details in here because it involves detailed DOM, DOM implementations, virtual DOM implementations and all that.所以我们就不去管这里面的细节了，因为这涉及到详细的DOM，DOM实现，虚拟DOM实现等等。
- look into 研究
- in a nutshell 简而言之
- granular adj.含颗粒的，颗粒状的； 粗糙的；
- in the sense that 
  - "In the sense that" is correctly used to distinguish between two possible senses (approximately meanings) of a word or phrase. So:"This fact is funny, in the sense that it makes me laugh" or "This fact is funny, in the sense that it is strange".
  - This phrase is an explanatory linking phrase, used to link two parts of a sentence together so that it is clear that the first statement is being explained by or contrasted with the second part.
- This is essentially a basic form of dependency tracking that's commonly shared in Knockout.js, Meteor Tracker, and Vue.js and MobX. MobX is a state management pattern for React.

### getters and setters

- essentially 本质上
- arbitrary values 任意值
- to assert whether your current implementation is correct 以确定您当前的实现是否正确
- access and assignments 访问和赋值
- And this class will have two methods, depend and notify 这个类会有两个方法，依赖和通知
- associate 关联
- go half through the time 时间过半
- So the catch here is 所以这里的问题是
- So this variable will always point to something that references this 所以这个变量将始终指向引用这个变量的东西

### dependency tracker
- That's the whole point, right? 这就是重点，对吧？
- so we can just take the subscriber function and just invoke it 所以我们可以直接使用订阅者函数并调用它
- That's pretty much it 这就差不多了
- this wrapped update 封装的更新
- we need to clean up stale dependencies 我们需要清理过时的依赖关系
- This is not accounted for 没有考虑到的

### mini observer
- mutate a property 改变一个属性
- fill in the blanks 填空
- to this point 到此为止



## intro writing plugins




### writing a simple plugin



### render functions




### 
(Essentially) A lightweight JavaScript data format to represent what the actual DOM should look like at a given point in time (本质上)一个轻量级的JavaScript数据格式来表示实际的DOM在一个给定的时间点应该是什么样子的。