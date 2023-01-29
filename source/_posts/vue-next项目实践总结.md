---
title: vue-next项目实践总结
date: 2021-04-27 15:50:15
tags:
---
> 起源Nov.2018 VueConf TO (Evan You) - Vue 3.0 Updates (faster,smaller,more maintainable,easier to target native)
```
尽可能兼容2.0 的API
之前Virtual DOM会有蛮多运行时开销的
生成更易被JS引擎优化的代码

判断原生还是组件
Component path fast

生成虚拟node的时候，函数尽量一致
优化slots生成
2.0 基于ES5的 getter，setter 进行 

Lazy by default
直接暴露给用户this 
API不动

Vue本身runtime更小

按需引入

最最基本的代码在10KB左右
降低源码阅读难度

Vetur
Vue hooks

框架做js计算-》浏览器主线程block-》无法响应用户事件

16ms（一frames）
明年下半年发布
```

> 在一个业务简单，逻辑清晰的项目里面，Vue-next作为开发框架
https://v3.cn.vuejs.org/guide/introduction.html

### devtools
商店里面下载Vue devtools 的 beta 版本，然后把之前的版本卸载掉
这个时候重新打开之前的Vue3的页面即可

项目里面配置：
```
// 打开浏览器工具
if (process.env.NODE_ENV === 'development') {
  if ('__VUE_DEVTOOLS_GLOBAL_HOOK__' in window) {
    // 这里__VUE_DEVTOOLS_GLOBAL_HOOK__.Vue赋值一个createApp实例
    ;(window as any).__VUE_DEVTOOLS_GLOBAL_HOOK__.Vue = app
  }
  const config: any = app.config
  config.devtools = true
}
```
这个是cli初始化项目时候带的

## basic
> 其实都是文档上写了的
#### 单文件组件<script setup>
- 普通的 <script> 只在组件被首次引入的时候执行一次
- <script setup> 中的代码会在每次组件实例被创建的时候执行
- 顶层的绑定会被暴露给模版

v3
1-7 12 14