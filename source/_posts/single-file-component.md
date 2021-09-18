---
title: single-file-component
date: 2021-09-18 14:38:08
tags:
---
### vue 2.x

- vue-template-compiler
- https://cn.vuejs.org/v2/guide/single-file-components.html


### vue 3.x
- @vue/sfc-compiler
- https://v3.cn.vuejs.org/guide/single-file-component.html#%E5%8D%95%E6%96%87%E4%BB%B6%E7%BB%84%E4%BB%B6
```
=>文档描述：
工作原理
Vue SFC 是框架指定的文件格式，必须由 @vue/compiler-sfc 预编译为标准的 JavaScript 与 CSS。编译后的 SFC 是一个标准的 JavaScript（ES）模块——这意味着通过正确的构建配置，可以像模块一样导入 SFC：

import MyComponent from './MyComponent.vue'

export default {
  components: {
    MyComponent
  }
}
SFC 中的 <style> 标签通常在开发过程中作为原生 <style> 标签注入以支持热更新。对于生产环境，它们可以被提取并合并到单个 CSS 文件中。

可以在 Vue SFC Playground 中使用 SFC ，探索其是如何编译的。

在实际项目中，通常会将 SFC 编译器与 Vite 或 Vue CLI（基于 webpack）等构建工具集成在一起，Vue 提供的官方脚手架工具，可让你更快地开始使用 SFC。查阅 SFC 工具 部分查看更多细节。
```

·
### tips
这个compiler的版本依赖于vue的版本，锁版本的时候注意，避免一个锁了，一个又有升级的宽容度（项目中出现过vue锁了版本，compiler没锁，但是没提示版本问题，编译出来的包Object（）,err）
