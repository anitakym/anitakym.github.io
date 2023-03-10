---
title: React-Component
date: 2023-02-17 17:27:34
tags:
---

## 类组件
#### 类组件底层只需实例化一次，实例中保存了组件的state等状态，更新只要调用render方法和对应的生命周期即可

#### react-reconciler/src/ReactFiberClassComponent.js
- constructClassInstance
```
export {
  adoptClassInstance,
  constructClassInstance,
  mountClassInstance,
  resumeMountClassInstance,
  updateClassInstance,
};
```

#### 
在 class 组件中，除了继承 React.Component ，底层还加入了 updater 对象，组件中调用的 setState 和 forceUpdate 本质上是调用了 updater 对象上的 enqueueSetState 和 enqueueForceUpdate 方法

- react/src/ReactBaseClasses.js



## 函数组件
#### 函数组件中，每次更新是新的函数执行，里面的变量会重新声明

#### react-reconciler/src/ReactFiberHooks.js
```
export function renderWithHooks<Props, SecondArg>
```


### references
#### getderivedstatefromprops
https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromprops

#### fiber tag
react-reconciler/src/ReactFiber.js
react-reconciler/src/ReactWorkTags.js
```
export const FunctionComponent = 0;
export const ClassComponent = 1;
```


### 组件通信方式
- props callback - 父组件通过props将信息传递给子组件，子组件可以通过执行props中的回调函数callback来触发父组件的方法
- ref
- react-redux | react-mobx 等状态管理工具
- context 上下文
- @event bus -> 适合用React做基础构建的小程序 - Taro
```
问题：
- 需要手动绑定和解绑
- 后期难以维护，组件之间状态未知
- 违背了React数据的流向的大原则
```

### 组件的强化方式
#### 类组件继承
- state和声明周期会被继承后的组件修改

#### 函数组件自定义hooks

#### HOC高阶组件




### reconciliation
- React渲染机制 - reconciliation过程
- props或state改变 - render函数返回不同的元素树 - 新旧DOM树diff - 针对差异的地方进行更新 - 渲染为真实的DOM树
- shouldComponentUpadate - 合理利用 - 避免不必要的reconciliation过程 - 类组件！- PureComponent - （props或state改变时进行浅层比较）
- memo - 函数组件 - 只进行了props的浅比较


### diff（不同React版本，也是持续优化中）
- 永远只比较同层节点 ｜ 不同的两个节点产生不同的树 ｜ 通过key值指定哪些元素是相同的 - O(n)
- 执行的具体流程（元素类型是否相同）
- 遍历子节点列表的情况（子节点是否有key）
- 选择key值策略 - 不需要全局统一，但必须列表


## HOC - 高阶组件

### Why
> 解决大量的代码复用，逻辑复用问题

#### 拦截问题
- 对渲染的控制(例如权限控制是否渲染)
- dva - dynamic - 懒加载/动态加载组件

#### props中混入需要的
- withRoute  - HOC 把改变路由的 history 对象混入 props 中

#### 监控组件的内部状态，赋能组件
- 监控组件内的事件
- 增加额外生命周期

### what
#### 基本概念
- 高阶组件是以组件作为参数，返回组件的函数。返回的组件把传进去的组件进行功能强化

#### 属性代理
- 用组件包裹一层代理组件，在代理组件上，可以做一些，对源组件的强化操作
- 返回的是一个新组件，被包裹的原始组件，将在新的组件里被挂载


#### 反向继承
- 包装后的组件继承了原始组件本身，所以无须再去挂载业务组件

### how
#### 强化props


#### 控制渲染
- 渲染劫持 - HOC 反向继承模式，可以通过 super.render() 得到 render 之后的内容，利用这一点，可以做渲染劫持 ，还可以修改 render 之后的 React element 对象
#### 动态加载 
- dva 中 dynamic 就是配合 import ，实现组件的动态加载的，而且每次切换路由，都会有 Loading 效果
#### 组件赋能
- ref获取实例
- 事件监控

### tips
- 谨慎修改原型链
- 不要在函数组件内部&&类组件render函数中使用
- 多个HOC嵌套，应该留意一下HOC的顺序，还要分析出要各个 HOC 之间是否有依赖关系
- 类组件，可以用装饰器模式，对类组件进行包装
- 属性代理 HOC 本质上返回了一个新的 component ，那么如果给原来的 component 绑定一些静态属性方法，如果不处理，新的 component 上就会丢失这些静态属性方法 - （手动继承 or hoist-non-react-statics）

### cases
- 管理后台，权限隔离