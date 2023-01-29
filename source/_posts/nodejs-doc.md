---
title: nodejs-doc
date: 2021-03-04 12:12:00
tags:
    - node
---
## latest
- corepack - https://github.com/nodejs/corepack
- undici WG - https://github.com/nodejs/undici
- diagnostics WG - 门槛更低的诊断能力
- Node-API WG - 现代化，API稳定的Addon API
- strategic-initiatives - https://github.com/nodejs/node/blob/main/doc/contributing/strategic-initiatives.md
- https://nodejs.org/calendar
## nodejs-path
### 文档指北：
https://nodejs.org/api/path.html#path_path
http://nodejs.cn/api/path.html
还是推荐dash,可以快速搜索，然后选择右上角copy online page

### 项目经验
node服务项目
electron项目

### globals
- https://nodejs.org/api/globals.html

### Module
- https://nodejs.org/api/packages.html



### querystring
- https://nodejs.org/dist/latest-v16.x/docs/api/querystring.html
```
/**
 * The `querystring` module provides utilities for parsing and formatting URL
 * query strings. It can be accessed using:
 *
 * ```js
 * const querystring = require('querystring');
 * ```
 *
 * The `querystring` API is considered Legacy. While it is still maintained,
 * new code should use the `URLSearchParams` API instead.
 * @deprecated Legacy
 * @see [source](https://github.com/nodejs/node/blob/v18.0.0/lib/querystring.js)
 */
```
- https://nodejs.org/dist/latest-v16.x/docs/api/url.html#class-urlsearchparams

### 基础架构（原理）


### api
#### vm
- https://nodejs.org/api/vm.html
- https://www.youtube.com/watch?v=u81pS05W1JY
- https://pwnisher.gitlab.io/nodejs/sandbox/2019/02/21/sandboxing-nodejs-is-hard.html
用这个实现基于ES6模版字符串语法语法的模版引擎
- 通过VM模块编译JS形成函数
    - include子模版
    - XSS过滤、模版helper函数

### npm
#### easy_sock


#### https://www.npmjs.com/package/protocol-buffers

### slides - ryan dahl 的一系列在conf里面的演讲，不同阶段，可以去YTB上面看
- nodejs ry@tinyclouds 2009 - 最初的设计，为什么这么设计
- https://www.slideshare.net/JSFestUA/js-fest-2019-ryan-dahl-deno-a-new-way-to-javascript

#### perf_hooks
perf_hooks
解决这个报warining的问题
先新建一个项目，引入perf_hooks,没有任何问题
看了不同版本的代码，发现引入的问题，升级了版本即可
http://nodejs.cn/api/perf_hooks.html