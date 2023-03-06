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
- render阶段render函数执行 - commit 阶段真实DOM替换 - setState回调函数执行cb
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
- enqueueSetState(类组件初始化过程中绑定了负责更新的Updater对象，调用 setState 方法，实际上是 React 底层调用 Updater 对象上的 enqueueSetState 方法)
```
/react-reconciler/src/ReactFiberClassComponent.js
react-dom/src/events/DOMLegacyEventPluginSystem.js
```
- React同一级别setState 更新优先级： flushSync > 正常执行上下文 > setTimeout > Promise
### 函数组件中的state

在 useState 的 dispatchAction 处理逻辑中，会浅比较两次 state ，发现 state 相同，不会开启更新调度任务；
- 如果直接改变state，在内存中指向的地址相同（state.name = 'b'）



### useState - 原理