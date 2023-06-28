---
title: react-项目总结
date: 2023-02-16 11:46:21
tags:
---
#### why
- 交互式UI-简单
- 组件化
- 跨平台

#### history - feature
`https://github.com/facebook/react/releases`
- v16.0 - 2017.09 
```
重写Reconciler - 性能，Fiber - 性能 ，createPortal API - 让节点渲染到指定容器内，更好实现弹窗功能 ，componentDidCatch -> 划分了错误边界，捕获渲染中的异常
```
- v16.2
```
React
Add Fragment as named export to React. (@clemmy in #10783) -> 解决数组元素问题
Support experimental Call/Return types in React.Children utilities. (@MatteoVH in #11422)

```
- v16.3
```
React
Add a new officially supported context API. (@acdlite in #11818)
Add a new React.createRef() API as an ergonomic alternative to callback refs. (@trueadm in #12162)
Add a new React.forwardRef() API to let components forward their refs to a child. (@bvaughn in #12346)
Fix a false positive warning in IE11 when using React.Fragment. (@XaveScor in #11823)
Replace React.unstable_AsyncComponent with React.unstable_AsyncMode. (@acdlite in #12117)
Improve the error message when calling setState() on an unmounted component. (@sophiebits in #12347)
```
- v16.6
```
React
Add React.memo() as an alternative to PureComponent for functions. (@acdlite in #13748) - 控制子组件的渲染
Add React.lazy() for code splitting components. (@acdlite in #13885) - 代码分割
React.StrictMode now warns about legacy context API. (@bvaughn in #13760)
React.StrictMode now warns about findDOMNode. (@sebmarkbage in #13841)
Rename unstable_AsyncMode to unstable_ConcurrentMode. (@trueadm in #13732)
Rename unstable_Placeholder to Suspense, and delayMs to maxDuration. (@gaearon in #13799 and @sebmarkbage in #13922)
React DOM
Add contextType as a more ergonomic way to subscribe to context from a class. (@bvaughn in #13728) - 方便类组件使用context
```
- v16.8 - Add Hooks — a way to use state and other React features without writing a class. (@acdlite et al. in #13968) - 使函数组件也能做类组件做的一切事儿
- v17 - 2020.10 - 事件绑定（document -> container ）, 移除事件池
`https://reactjs.org/blog/2020/10/20/react-v17.html`


#### react-scripts
- https://www.npmjs.com/package/react-scripts
- @svgr/webpack
```
This package includes scripts and configuration used by Create React App.
Please refer to its documentation:
```

#### better-scroll
```
BetterScroll 是一款重点解决移动端（已支持 PC）各种滚动场景需求的插件。它的核心是借鉴的 [iscroll](https://github.com/cubiq/iscroll) 的实现，它的 API 设计基本兼容 iscroll，在 iscroll 的基础上又扩展了一些 feature 以及做了一些性能优化。

BetterScroll 是使用纯 JavaScript 实现的，这意味着它是无依赖的。
```
- https://github.com/ustbhuangyi/better-scroll


#### react-lazyload

#### react-flow
- https://github.com/wbkd/react-flow
- 高度可定制的库，用于构建基于节点的交互式用户界面、工作流程编辑器、流程图或静态图

#### react-transition-group

#### @emotion/react
Emotion is a library designed for writing css styles with JavaScript. It provides powerful and predictable style composition in addition to a great developer experience with features such as source maps, labels, and testing utilities. Both string and object styles are supported.


## 优化
