---
title: module之commonjs与ES6及其他
date: 2021-01-06 13:51:11
tags:
---

### 兼容性
- https://caniuse.com/es6-module
- 现在看起来还行昂，越来越好了

参考文档：https://www.zhihu.com/question/20351507/answer/14859415

http://caibaojian.com/es6/module.html

项目经历：
node:commonjs
foreceipt:amd(requirejs)
现在项目：es6

### systemjs
- https://babeljs.io/docs/babel-plugin-transform-modules-systemjs  This plugin is included in @babel/preset-env under the modules option(@vitejs/plugin-legacy -> @babel/preset-env)
- vite - legacy - systemjs

- cocos creator里面，对于模块的处理，使用了systemjs
- https://github.com/systemjs/systemjs/blob/main/docs/system-register.md