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