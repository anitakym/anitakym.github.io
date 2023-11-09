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

### babel-plugin
- https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md


### @babel/traverse
- 用于遍历和更新抽象语法树（Abstract Syntax Tree，AST）
- "@babel/traverse" 的模块对于做语法分析、代码转化、代码生成等任务非常实用。

在 Babel 的转换流程中，“解析”阶段会生成一棵 AST，然后 "@babel/traverse" 在“转换”阶段遍历这棵 AST，根据需要进行各种转换。你可以在插件或 preset 中使用它，以实现你想要的转换。

```javascript
import * as parser from "@babel/parser";
import traverse from "@babel/traverse";
const code = "function square(n) { return n * n; }";
const ast = parser.parse(code);

traverse(ast, {
  enter(path) {
    if (path.isIdentifier({ name: "n" })) {
      path.node.name = "x";
    }
  }
})
```