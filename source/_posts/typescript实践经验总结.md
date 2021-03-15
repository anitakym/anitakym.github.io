---
title: typescript实践经验总结
date: 2021-03-08 12:07:02
tags:
---

几个迁移的案例
https://developers.google.com/web/updates/2021/01/puppeteer-typescript


redaxios
https://www.tslang.cn/docs/handbook/type-checking-javascript-files.html
https://github.com/Microsoft/TypeScript/wiki/JSDoc-support-in-JavaScript
使用JSDoc注解
```
// https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html
支持的JSDoc
下面的列表列出了当前所支持的JSDoc注解，你可以用它们在JavaScript文件里添加类型信息。

注意，没有在下面列出的标记（例如@async）都是还不支持的。

@type
@param (or @arg or @argument)
@returns (or @return)
@typedef
@callback
@template
@class (or @constructor)
@this
@extends (or @augments)
@enum
它们代表的意义与usejsdoc.org上面给出的通常是一致的或者是它的超集。 
```