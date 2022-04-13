---
title: eslint版本问题
date: 2021-03-22 18:18:33
tags:
---

### 命令行脚本
- npm run lint:init
- ```eslint --init```
- 初始化配置 - interactive
- npm run lint:fix 
- ```eslint './**/*.js' --fix```
### basics
#### env
- browser: true - 就告诉eslint,是浏览器项目，这样不会有console未定义这样的错误（浏览器内置对象）
#### rules
- 定义覆盖规则

### Vscode
- 编辑器给出语法提示
#### parserOptions
- 指定支持的版本的最新的语法 - ecmaVersion
- 支持ES module模块加载语法的检查 - sourceType: 'module'
### problems
Cannot read property 'range' of null

babel-eslint版本依赖问题

删除了node_modules和package-lock.json文件，重新安装后，问题就没有了

```
warning  in ./src/views/statistical/english/data.js

Module Warning (from ./node_modules/thread-loader/dist/cjs.js):
Cannot read property 'range' of null

```

#### eslint版本问题
- 如果是在Linux机器上，16.x的node版本，安装之前用低版本