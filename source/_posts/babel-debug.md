---
title: babel-debug
date: 2022-11-17 11:38:55
tags:
---


## 插件机制

- babel 插件 - 进一步封装成了预设（preset）, out of box

### core
- babel本身的优势在于可以实现各种插件，从而解析和转换JS代码
### 原理
- babel -> JavaScript代码转换器（transpiler）
- Abstract Syntax Tree 抽象语法树
- code PARSE(解析 -> Abstract Syntax Tree)
- TRANSFORM（transpile-转换 -> 对AST进行 traverse&&replace）
- GENERATE（生成 -> 根据新的AST生成编译后的code） code
- babel插件的作用 - 在上面的过程中，对AST进行修改，从而达到转换的目的

### cases

#### 简化向量运算
- https://spritejs.com/#/
- https://github.com/toji/gl-matrix
- https://www.npmjs.com/package/babel-plugin-transform-gl-matrix
- 测试先行