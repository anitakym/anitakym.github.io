---
title: 深入浅出Vuejs-精读
date: 2021-05-24 10:40:18
tags:
---
## 序
是我很喜欢的月影和松峰老师作序
月影老师序：
"所谓元编程，简单来说，是指框架的作者使用一种编程语言固有的语言特性，创造出相对新的语言特性，使得最终使用者能够以新的语法和语义来构建他们的应用程序，从而在某些领域开发中获得更好的开发体验。"
"jQuery仅仅通过巧妙设计API就能支持上述特性(链式语法和隐式迭代语义)，并不依赖于编程语言赋予的元编程能力"
"JavaScript自身提供了许多元编程特性，比如从ES5就开始支持的属性访问器（property accessor），ES6支持的代理（proxy），还有标准提案已经处于Stage 3阶段的装饰器（decorator）"
"如何设计API和如何使用元编程思想将新特性融入到框架中，是现代JavaScript框架设计的两个核心，Vue.js更侧重于后者"
要考虑的细节：
- 向下兼容
- 性能
学习Vue.js，掌握设计应用程序框架的一般性技巧，还可以在实现应用程序时运用其中的具体设计思想和方法论。
松峰老师序：
"当时我说，要想让技术书畅销，一是读者定位必须是新手，因为新手人数众多；二是要注重实用，书中的例子最好能立即照搬到项目上。"

## 前言
"Vue.js也是如此，它解决了什么问题？如何解决的？解决问题的同时都做了哪些权衡和取舍？"

- DOM操作 - 命令式 => 声明式
- 渐进式 - Vue.js / +router / +vuex / +vue-cli
  - Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架
  - 渐进式框架 - 把框架分层 - 核心是视图层渲染 + 组件机制 + 路由机制 + 状态管理 + 构建工具
- 单文件组件 - 很棒的一个feature（https://cn.vuejs.org/v2/guide/single-file-components.html）
- The fate of destruction is also the joy of rebirth - 1.x
- Your effor to remain what your are is what limits you - 2.x - Masamune Shirow, Ghost in the Shell
  - 引入虚拟DOM
  - 支持JSX和TS
  - 支持流式服务端渲染
  - 提供跨平台能力
- Just a view layer library（Vue 的核心库只关注视图层）
- 关于Vue.js
  - 学习曲线和API设计 - 优雅，简单 -> 竞争力
  - Chrome开发者插件使用情况
  - 社区 - Nuxt,Quasar Framework, Element,iView,Muse-UI,Vux,Vuetify,Vue Material

## 变化侦测
> 理解原理帮助我们规避问题
- reactive(feature)
