---
title: 工作中遇到的babel
date: 2020-11-28 20:26:03
tags:
---

### why && what 
- babel是JavaScript编译器
- 解决代码对旧版本的兼容性问题

### 初始化项目
- @vue/cli 的话，可以直接走```@vue/cli-plugin-babel```
- 没用脚手架构建工具的话： @babel/core - 核心库 @babel/cli - 命令行工具 @babel/preset-env - 默认的预设环境 | devDependencies
- core-js - dependencies - 在运行时为老版本的浏览器提供不支持的API

### .babelrc
- 


### 
### 官方文档
https://babeljs.io/
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


## 开发babel插件
### 原理
#### 解析阶段
- 词法分析（tokens）
- 语法分析（AST）
#### 转换阶段
- 访问者模式
- 深度优先遍历
- path
#### 生成阶段



## cases
### vue2.x的项目
- 要使用 ```<script setup>``` 的语法，所以引用了插件 
- https://github.com/antfu/unplugin-vue2-script-setup.git
- https://github.com/antfu/unplugin-vue2-script-setup/blob/main/src/core/transformScriptSetup.ts
- 处理script setup语法支持的时候
```
import generate from '@babel/generator'
return {
    ast,
    code: generate(ast).code,
  }

```

### shippedproposal
https://github.com/vitejs/vite/commit/ed25817
https://tc39.es/ecma262/#sec-array.prototype.at
https://tc39.es/ecma262/2021/
https://tc39.es/ecma262/2022/

### compat-table
https://kangax.github.io/compat-table/es2016plus/


### Presets
@babel/preset-env

基本上可以看到各个版本的新增特性和用法
https://babeljs.io/docs/babel-plugin-transform-async-to-generator