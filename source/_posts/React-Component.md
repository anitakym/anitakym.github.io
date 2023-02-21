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