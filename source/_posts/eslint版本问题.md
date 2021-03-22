---
title: eslint版本问题
date: 2021-03-22 18:18:33
tags:
---
Cannot read property 'range' of null

babel-eslint版本依赖问题

删除了node_modules和package-lock.json文件，重新安装后，问题就没有了

```
warning  in ./src/views/statistical/english/data.js

Module Warning (from ./node_modules/thread-loader/dist/cjs.js):
Cannot read property 'range' of null

```