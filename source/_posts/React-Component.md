---
title: React-Component
date: 2023-02-17 17:27:34
tags:
---

## 类组件
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