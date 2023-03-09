---
title: react-lifecycle
date: 2023-03-06 17:43:54
tags:
---
> React 类组件 - 生命周期钩子函数

## React 阶段
- React 在调和( render )阶段会深度遍历 React fiber 树 -> 发现不同( diff )，不同的地方就是接下来需要更新的地方，对于变化的组件，就会执行 render 函数
- 在一次调和过程完毕之后，就到了commit 阶段，commit 阶段会创建修改真实的 DOM 节点
- 调和的过程中，发现了一个 fiber tag = 1 类组件的情况，就会按照类组件的逻辑来处
- react-reconciler/src/ReactFiberBeginWork.js
- 组件初始化 ｜ 组件更新 ｜ 组件销毁
### 初始化阶段
#### render阶段
- constructor（constructClassInstance，mountClassInstance） ｜ getDerivedStateFromProps | componentWillMount | render

#### commit阶段(before mutation | mutation | layout)
- 更新DOM ｜ componentDidMount（react-reconciler/src/ReactFiberCommitWork.js）

### 更新阶段
- componentWillReceiveProps ｜ getDerivedStateFromProps ｜ shouldComponentUpdate ｜ componentWillUpdate ｜ getSnapshotBeforeUpdate ｜ componentDidUpdate

### 销毁阶段
- componentWillUnmount

## 具体API
#### constructor
- 在类组件创建实例时调用
- 初始化state ｜ 对类组件的事件做处理（绑定this，节流，防抖）
- 生命周期劫持，渲染劫持（HOC）

#### getDerivedStateFromProps
- getDerivedStateFromProps(nextProps,prevState)
- 在初始化和更新阶段，接受父组件的 props 数据， 可以对 props 进行格式化，过滤等操作，返回值将作为新的 state 合并到 state 中，供给视图渲染层消费
- componentWillMount 和 componentWillReceiveProps  替代

#### unsafe
- React V16.3 componentWillMount ，componentWillReceiveProps ， componentWillUpdate
- 在render之前执行
- componentWillReceiveProps（一个思路 - 可以做一个状态提升，数据层托管父组件，子组件无副作用只负责渲染props）
- PureComponent在 componentWillReceiveProps 执行之后浅比较 props 是否发生变化
- getSnapshotBeforeUpdate 来代替 UNSAFE_componentWillUpdate

#### render
- 一次 render 的过程，就是创建 React.element 元素的过程
- render -> createElement创建元素 , cloneElement 克隆元素 ，React.children 遍历 children 的操作


#### getSnapshotBeforeUpdate
- 在 commit 阶段的before Mutation ( DOM 修改前)
- 配合componentDidUpdate 一起使用，计算形成一个 snapShot 传递给 componentDidUpdate ,保存一次更新前的信息

#### componentDidUpdate
- DOM 已经更新，可以直接获取 DOM 最新状态
- 如果使用 setState ，一定要加以限制，否则会引起无限循环
- 接受 getSnapshotBeforeUpdate 保存的快照信息


#### componentDidMount
- 做一些关于 DOM 操作，比如基于 DOM 的事件监听器
- 初始化向服务器请求数据，渲染视图

#### shouldComponentUpdate
- 性能优化
- 如果有 getDerivedStateFromProps 生命周期 ，它的返回值将合并到 newState ，供 shouldComponentUpdate 使用


#### componentWillUnmount
- 清除延时器，定时器
- 一些基于 DOM 的操作，比如事件监听器

## 函数组件

### API
#### useEffect
- 异步调用 ，对于每一个 effect 的 callback， React 会放入任务队列，等到主线程任务完成，DOM 更新，js 执行完成，视图绘制完毕，才执行
- effect 回调函数不会阻塞浏览器绘制视图


#### useLayoutEffect
- 同步执行
- 在 DOM 更新之后，浏览器绘制之前
- callback 中代码执行会阻塞浏览器绘制

#### useInsertionEffect - v18
- 解决 CSS-in-JS 在渲染中注入样式的性能问题


## 对比

### componentDidMount | useEffect
```
React.useEffect(()=>{
    /* 请求数据 ， 事件监听 ， 操纵dom */
},[])  /* dep = [] */

```

### componentWillUnmount | useEffect
```
 React.useEffect(()=>{
        /* 请求数据 ， 事件监听 ， 操纵dom ， 增加定时器，延时器 */
        return function componentWillUnmount(){
            /* 解除事件监听器 ，清除定时器，延时器 */
        }
},[])/* dep = [] */
```

### componentWillReceiveProps
```
React.useEffect(()=>{
    console.log('props变化：componentWillReceiveProps')
},[ props ])
React.useEffect(()=>{
    console.log('props变化：componentWillReceiveProps')
},[ props.abc ])
```

### componentDidUpdate - 同步执行，commit阶段
```
异步执行，commit阶段
React.useEffect(()=>{
    console.log('组件更新完成：componentDidUpdate ')     
}) /* 没有 dep 依赖项 */
// 没有第二个参数，那么每一次执行函数组件，都会执行该 effect
```