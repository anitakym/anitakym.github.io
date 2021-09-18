---
title: typescript实践经验总结
date: 2021-03-08 12:07:02
tags:
---

### 几个迁移的案例
https://developers.google.com/web/updates/2021/01/puppeteer-typescript


### redaxios
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

### 推荐相关文档：
https://zhuanlan.zhihu.com/p/40322215
https://labs.thisdot.co/blog/your-first-vue-3-app-using-typescript
https://medium.com/vue-typescript/vue-3-with-typescript-setup-a-new-project-with-the-vue-cli-4ea806be7a91


### 推荐TS入门：
https://basarat.gitbook.io/typescript/getting-started
https://jkchao.github.io/typescript-book-chinese/typings/types.html#%E4%BD%BF%E7%94%A8-types

### 教程推荐
- 英文OK的还是官方文档
    - https://www.typescriptlang.org/docs/handbook/basic-types.html
    - 更新及时，对应版本准确
- 中文的话：
    - http://ts.xcatliu.com/


## 项目总结

### 接入的第三方插件
#### sentry
- sentry本身就有@sentry/types，被JavaScript 相关的 SDK依赖，所以没啥问题，安装之后，就支持了
- https://getsentry.github.io/sentry-javascript/