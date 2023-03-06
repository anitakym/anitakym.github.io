---
title: react-props
date: 2023-03-06 17:06:38
tags:
---
> react中的props

### React组件层级
- 父组件把数据层传递给子组件渲染消费
- 子组件通过props中的callback，向父组件传递信息
- 将视图容器作为props进行渲染


### React更新机制
- props 可以作为组件是否更新的重要准则，变化即更新（ PureComponent ，memo ）

### React插槽
- React 可以把组件的闭合标签里的插槽，转化成 Children 属性


### 监听props改变
#### 类组件 - unsafe_componentWillReceiveProps
```
If you define UNSAFE_componentWillReceiveProps, React will call it when the component receives new props. It only exists for historical reasons and should not be used in any new code. Instead, use one of the alternatives
在16.3.0中被标记为unsafe
在16.9.X中被废除，新增功能处理不要使用了
因为这个生命周期超越了 React 的可控制的范围内，可能引起多次执行等情况发生
每次父组件更新都会触发当前组件的componentWillRecieveProps
getDerivedStateFromProps - 组件一旦使用派生状态，很有可能因为没有明确的数据来源导致出现一些bug和不一致性，理解场景，正确使用
官方根据不同使用场景，给出的替代方案（https://beta.reactjs.org/reference/react/Component#unsafe_componentwillreceiveprops）

https://reactjs.org/docs/react-component.html#unsafe_componentwillreceiveprops
```
#### 函数组件 - useEffect


### props children模式
#### prop + child
- props插槽组件 ｜ render props模式 ｜ 混合模式
- react-router (Switch, Route) - The `<Routes>` component recurses through its `props.children`, strips their props, and generates an object like this
- antd (Form , FormItem)

### skills
- 抽象props
- 抽离props
- 注入props
- 隐式注入props