---
title: immutable-summary
date: 2023-03-01 11:22:28
tags:
---
> Dan Abramov : Only copy the parts that actually changed.Libraries like immutability-helper,updeep,immer help with this

- immutable - 利用结构共享形成的持久化数据结构，一旦有部分被修改，那么将会返回一个全新的对象，并且原来相同的节点会直接共享

- immutable 对象数据内部采用是多叉树的结构，凡是有节点被改变，那么它和与它相关的所有上级节点都更新

## immutable
### fromJS
### toJS
- 需要让immutable对象调用


## 结合Redux使用
- https://immutable-js.com/
- 官方文档
- https://github.com/gajus/redux-immutable
- 按usage操作即可