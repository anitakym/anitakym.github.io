---
title: webComponents
date: 2022-02-11 16:06:06
tags:
---
- https://developer.mozilla.org/zh-CN/docs/Web/Web_Components
- github - https://github.com/WICG/webcomponents
- https://github.com/webcomponents/polyfills/tree/master/packages/webcomponentsjs - polyfill相关
- https://lit.dev/ - framework
- https://zh-hans.reactjs.org/docs/web-components.html



### Tips
根据需要适配的浏览器，做好适配
如果不处理，edge会直接抛错，阻塞渲染
- As a workaround, if your project has been compiled to ES5, load custom-elements-es5-adapter.js before defining Custom Elements. This adapter will automatically wrap ES5.

### omi - Web Components Framework - Web组件框架
- https://github.com/Tencent/omi
```
📶 信号 Signal 驱动的响应式编程，reactive-signal强力驱动
⚡ 微小的尺寸，极速的性能
💗 目标 100+ 模板 & OMI 模板源码
🐲 OMI Form & OMI Form 游乐场 & Lucide Omi 图标
🌐 你要的一切都有: Web Components, JSX, Function Components, Router, Suspense, Directive, Tailwindcss...
💯 面向对象编程(OOP) 和 数据驱动编程(DOP) 两种范式都支持
💒 使用 Constructable Stylesheets 轻松管理和共享样式
```