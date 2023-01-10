---
title: vue-next项目实践总结
date: 2021-04-27 15:50:15
tags:
---
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