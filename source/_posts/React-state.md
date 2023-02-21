---
title: React-state
date: 2023-02-20 16:32:16
tags:
---
#### React mode
- legacy
- blocking(concurrent的优雅降级和过渡版本)
- concurrent

> 下面的state，是基于legacy模式

### 类组件中的state
#### setState
- `setState(updater[, callback])`
- https://reactjs.org/docs/react-component.html#setstate
- https://zh-hans.reactjs.org/docs/faq-state.html
#### 类组件限制state更新视图
- pureComponent对state和props进行浅比较，如果没有发生变化，组件不更新
```
/**
 * Convenience component with default shallow equality check for sCU.
 */
function PureComponent(props, context, updater) {
  this.props = props;
  this.context = context;
  // If a component has string refs, we will assign a different object later.
  this.refs = emptyObject;
  this.updater = updater || ReactNoopUpdateQueue;
}
```
- shouldComponentUpdate - 通过判断state变化来决定组件是否更新
- enqueueSetState
```
/react-reconciler/src/ReactFiberClassComponent.js
react-dom/src/events/DOMLegacyEventPluginSystem.js
```
