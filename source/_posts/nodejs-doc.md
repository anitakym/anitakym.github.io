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