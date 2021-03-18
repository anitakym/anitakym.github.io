---
title: 工作中遇到的babel
date: 2020-11-28 20:26:03
tags:
---
### 场景：
1. babel的升级—— 那么前提就要了解版本之间的核心差异，可以通过官方发布的blog，对整体概况有一个了解
2. 开发babel插件

### babel 7.0 的更新
https://babeljs.io/blog/2018/08/27/7.0.0
Babel 7.0 版本的重大变更包括：
- 支持 TypeScript 和 JSX Fragment；
- 不再支持没有维护的 Node 版本（0.10、0.12、4、5）；
- 使用 @babel 命名空间（babel-core 变成了 @babel/core）；
- 移除并停止发布任何年度预设（preset-es2015 等）;
- 移除“Stage” 预设（@babel/preset-stage-0 等）；
- 重命名了某些包（任何 TC39 提议插件现在都是 -proposal 而不是 -transform）。


### 开发babel插件