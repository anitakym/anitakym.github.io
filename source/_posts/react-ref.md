---
title: react-ref
date: 2023-03-06 18:33:14
tags:
---
## Ref对象创建
#### 类组件React.createRef
- react/src/ReactCreateRef.js
- 类组件有instance 能够维护像 ref 这种信息
#### 函数组件 useRef
- useRef 产生的 ref 对象挂到函数组件对应的 fiber 上，函数组件每次执行，只要组件不被销毁，函数组件对应的 fiber 对象一直存在，所以 ref 等信息就会被保存下来

## React本身对Ref的处理
> React对Ref属性的处理 - 标记ref

#### 类组件获取Ref的三种方式
- Ref属性是一个字符串
- Ref属性是一个函数
- Ref属性是一个ref对象

## ref高阶用法
#### forwardRef
- 解决ref不能跨层级捕获和传递的问题
- forwardRef接受父级元素标记的ref信息，并把它转发下去，使子组件可以通过props来接受到上面层级的ref
```
- 跨层级获取
- 合并转发ref
forwardRef 让 ref 可以通过 props 传递
如果用 ref 对象标记的 ref ，那么 ref 对象可以通过 props 的形式，提供给子孙组件消费
子孙组件也可以改变 ref 对象里面的属性
绑定在 ref 对象上的属性，不限于组件实例或者 DOM 元素，也可以是属性值或方法
- 高阶组件转发 higer-order components
```

#### ref实现组件通信
- 数据层托管层组件 - antd -form
```
类组件ref
函数组件forwardRef + useImperativeHandle
函数组件缓存数据 - useRef(useRef 可以创建出一个 ref 原始对象，只要组件不销毁，ref 对象就一直存在，可以把不依赖于视图更新的数据储存到 ref 对象中)
```

#### ref原理
- commitDetachRef
- commitAttachRef
- safelyDetachRef
- safelyAttachRef
- 如果是字符串 ref="node" 或是 函数式 ref={(node)=> this.node = node } 会执行 ref 函数，重置新的 ref 
- react-reconciler/src/ReactChildFiber.js
- react-reconciler/src/ReactFiberCommitWork.js
