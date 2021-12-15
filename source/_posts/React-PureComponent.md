---
title: React-PureComponent
date: 2021-12-15 10:21:31
tags:
---
> 当我们在React中，搜React.pureComponent时，
https://github.com/facebook/react/pull/7195

### changelog
以下两处
```
## 15.3.0 (July 29, 2016)

### React
- Add `React.PureComponent` - a new base class to extend, replacing `react-addons-pure-render-mixin` now that mixins don't work with ES2015 classes. ([@sophiebits](https://github.com/sophiebits) in [#7195](https://github.com/facebook/react/pull/7195))

## 16.1.0 (November 9, 2017)
### React Test Renderer and Test Utils

* Handle `forceUpdate()` and `React.PureComponent` correctly. ([@koba04](https://github.com/koba04) in [#11440](https://github.com/facebook/react/pull/11440))

```

### 为什么提供这个
- https://github.com/facebook/react/pull/7195

#### sophiebits commented on 6 Jul 2016
This provides an easy way to indicate that components should only rerender when given new props, like PureRenderMixin. If you rely on mutation in your React components, you can continue to use React.Component.

Inheriting from React.PureComponent indicates to React that your component doesn't need to rerender when the props are unchanged. We'll compare the old and new props before each render and short-circuit if they're unchanged. It's like an automatic shouldComponentUpdate.

## doc
```
React.PureComponent
React.PureComponent 与 React.Component 很相似。两者的区别在于 React.Component 并未实现 shouldComponentUpdate()，而 React.PureComponent 中以浅层对比 prop 和 state 的方式来实现了该函数。

如果赋予 React 组件相同的 props 和 state，render() 函数会渲染相同的内容，那么在某些情况下使用 React.PureComponent 可提高性能。

注意

React.PureComponent 中的 shouldComponentUpdate() 仅作对象的浅层比较。如果对象中包含复杂的数据结构，则有可能因为无法检查深层的差别，产生错误的比对结果。仅在你的 props 和 state 较为简单时，才使用 React.PureComponent，或者在深层数据结构发生变化时调用 forceUpdate() 来确保组件被正确地更新。你也可以考虑使用 immutable 对象加速嵌套数据的比较。

此外，React.PureComponent 中的 shouldComponentUpdate() 将跳过所有子组件树的 prop 更新。因此，请确保所有子组件也都是“纯”的组件。
```

## 参考阅读
- https://reactjs.org/blog/2016/07/13/mixins-considered-harmful.html