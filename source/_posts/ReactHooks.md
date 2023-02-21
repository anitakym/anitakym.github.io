---
title: ReactHooks
date: 2021-07-27 10:32:27
tags:
---

### react组件的演化
- 组件复用方式
- （类组件-class）
- （Mixin）
- (高阶组件-HOC) - 装饰器模式
- （Hooks）

## 基础
### React Router
- 
```
If you're using React Router, you should never import anything directly from the react-router package, but you should have everything you need in either react-router-dom or react-router-native. Both of those packages re-export everything from react-router.
```
- web用react-router-dom，react native 用react-router-native
- connected-react-router - https://www.npmjs.com/package/connected-react-router - A Redux binding for React Router v4 and v5
- connected-react-router - Synchronize router state with redux store through uni-directional flow (i.e. history -> store -> router -> components).
- https://reactrouter.com/docs/en/v6/upgrading/v5 - withRouter 的使用变更，可以用hooks代替



## 项目
- https://github.com/Netflix/metaflow-ui


## ref
- https://reactjs.org/docs/refs-and-the-dom.html
- https://reactjs.org/docs/hooks-reference.html#useref
- https://reactjs.org/docs/hooks-faq.html#how-can-i-measure-a-dom-node

