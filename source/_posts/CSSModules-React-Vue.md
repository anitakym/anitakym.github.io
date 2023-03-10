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

## CSS模块化
- 防止全局污染，样式覆盖
- 命名混乱
- CSSS代码冗余
### React CSS模块化
- CSS module
- css in js

#### CSS module
- css-loader配置
- 自定义命名规则
- 全局变量
- 组合样式
- 配置less和sass
- 全局或者公共组件样式，用.css文件
- 页面和业务组件，用scss｜less
- 配合classNames库，实现更灵活的动态添加类名

#### CSS module使用tips
- 仅用 class 类名定义 css ，不使用其他选择器
- 不要嵌套 css .a{ .b{} } 或者重叠 css .a .b {} 

#### CSS in JS
- CSS IN JS 本质上 - 用 js 中对象形式保存样式
- 拓展运算符实现样式继承
- style-components - 基于 props 动态添加样式 - https://styled-components.com/docs/