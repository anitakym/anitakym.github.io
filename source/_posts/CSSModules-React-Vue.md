---
title: CSSModules-React-Vue
date: 2021-11-29 18:25:57
tags:
---
> 最近做新项目，涉及多个团队，查问题的时候用上了我的样式搜索定位大法，诶，搜不到，哦，原来搜的关键词不准确，拉了代码瞅瞅，React组用了 CSS Modules

## React - Usages
- https://github.com/camsong/blog/issues/5

- react-app-rewired 插件支持
- creat-react-app , webpack css-loader 里面 modules 进行设置

## Vue - Usages
- https://vue-loader.vuejs.org/zh/guide/css-modules.html#%E7%94%A8%E6%B3%95
- 看上面文档来就行
- 现在项目脚手架默认生成配置用的是scoped CSS

## CSS moudles
- 原理：class名 hash值
- https://github.com/css-modules/css-modules
```
Webpack's css-loader in module mode replaces every local-scoped identifier with a global unique name (hashed from module name and local identifier by default) and exports the used identifier.
```
composition 组合 compose 嵌套
- BEM
Block  Element  Modifier => 模块名 节点名 节点状态 => name local hash:base64
- 公用样式｜局部化

### styled-components
- Visual primitives for the component age.
Use the best bits of ES6 and CSS to style your apps without stress
- 适合React - all in js
- https://github.com/styled-components/awesome-styled-components
- 如果要用iconfont的话，需要处理iconfont对应的文件