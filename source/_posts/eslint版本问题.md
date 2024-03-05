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


#### rules
- rules - https://eslint.org/docs/latest/user-guide/configuring/rules
- https://eslint.org/
```
"off" or 0 - turn the rule off
"warn" or 1 - turn the rule on as a warning (doesn’t affect exit code)
"error" or 2 - turn the rule on as an error (exit code is 1 when triggered)
```

### eslint-config
- https://github.com/antfu/eslint-config#faq


### eslint 和 prettier
- https://eslint.org/blog/2023/10/deprecating-formatting-rules/

```
旧项目
member-delimiter-style
DEPRECATED
Formatting rules now live in eslint-stylistic. @stylistic/ts/member-delimiter-style is the replacement for this rule.
See Deprecating Formatting Rules for more information.
```