---
title: typescript实践经验总结
date: 2021-03-08 12:07:02
tags:
---
> 多看下生成的JS，从而看看处理的逻辑（使用不同的ES标准进行编译）
### 几个迁移的案例
https://developers.google.com/web/updates/2021/01/puppeteer-typescript


### react-typescript
- https://github.com/typescript-cheatsheets/react
- https://react-typescript-cheatsheet.netlify.app/docs/basic/setup
### ROI 
- 团队迁移成本
（开发思维，开发生态，项目处理，接口及声明文件的维护）


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


### type vs interface
官方example
```
// There are two main tools to declare the shape of an
// object: interfaces and type aliases.
//
// They are very similar, and for the most common cases
// act the same.

type BirdType = {
  wings: 2;
};

interface BirdInterface {
  wings: 2;
}

const bird1: BirdType = { wings: 2 };
const bird2: BirdInterface = { wings: 2 };

// Because TypeScript is a structural type system,
// it's possible to intermix their use too.

const bird3: BirdInterface = bird1;

// They both support extending other interfaces and types.
// Type aliases do this via intersection types, while
// interfaces have a keyword.

type Owl = { nocturnal: true } & BirdType;
type Robin = { nocturnal: false } & BirdInterface;

interface Peacock extends BirdType {
  colourful: true;
  flies: false;
}
interface Chicken extends BirdInterface {
  colourful: false;
  flies: false;
}

let owl: Owl = { wings: 2, nocturnal: true };
let chicken: Chicken = { wings: 2, colourful: false, flies: false };

// That said, we recommend you use interfaces over type
// aliases. Specifically, because you will get better error
// messages. If you hover over the following errors, you can
// see how TypeScript can provide terser and more focused
// messages when working with interfaces like Chicken.

owl = chicken;
chicken = owl;

// One major difference between type aliases vs interfaces
// are that interfaces are open and type aliases are closed.
// This means you can extend an interface by declaring it
// a second time.

interface Kitten {
  purrs: boolean;
}

interface Kitten {
  colour: string;
}

// In the other case a type cannot be changed outside of
// its declaration.

type Puppy = {
  color: string;
};

type Puppy = {
  toys: number;
};

// Depending on your goals, this difference could be a
// positive or a negative. However for publicly exposed
// types, it's a better call to make them an interface.

// One of the best resources for seeing all of the edge
// cases around types vs interfaces, this stack overflow
// thread is a good place to start:

// https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/52682220#52682220

```


### declare
- https://www.typescriptlang.org/docs/handbook/declaration-files/by-example.html
#### declare module 'xxx'
- 声明一个全局模块
- 解决查找模块路径的问题
```
# env.d.ts

/// <reference types="vite/client" />

declare module '*.vue' {
  import type { DefineComponent } from 'vue'
  // eslint-disable-next-line @typescript-eslint/no-explicit-any, @typescript-eslint/ban-types
  const component: DefineComponent<{}, {}, any>
  export default component
}
```
- 环境声明 - *.d.ts文件, 里面每个根级别的声明需要以declare作为前缀

### 当你安装TypeScript时，会顺带安装一个lib.d.ts声明文件。这个文件包含JavaScript运行时及DOM（Document Object Model，文档对象模型）中存在的各种常见的JavaScript环境声明。● 它自动包含在TypeScript项目的编译上下文中。● 它能让你快速开始书写经过类型检查的JavaScript代码。
## tsconfig
- strictNullCheck 建议设置true，如果有需要都允许的地方，可以使用联合类型


## sources
- https://drive.google.com/file/d/170oHzpLNeprUa-TMmOAnSU4caEFDSb3e/view
- https://github.com/mike-works/typescript-fundamentals/tree/v2#dependencies


## why
> 用typescript的原因，是一种思维模式上面的减负；想应该想的，一些语言特性里面的遗留问题，不需要再想
```
undefined == null // true 
undefined === null // false
```
https://github.com/lodash/lodash.git

#### 注释
```
TypeScript 的 3.7 版本引入了 @ts-nocheck 注释，可以增加在 TypeScript 文件的头部来禁用语义检查。我们没有使用这个注释，因为它之前不支持.ts/.tsx 文件，但它也可以在迁移过程中成为一个很好的中间阶段助手。

TypeScript 的 3.9 版本引入了 @ts-expect-error 注释。当一行以 @ts-expect-error 注释作为前缀时，TypeScript 将禁止报告该错误。如果没有错误，TypeScript 会报告 @ts-expect-error 是不必要的。在 Airbnb 代码库，我们使用了 @ts-expect-error 而不是 @ts-ignore 。
https://medium.com/airbnb-engineering/ts-migrate-a-tool-for-migrating-to-typescript-at-scale-cd23bfeb5cc​​​
```

### Prototypes
- https://gist.github.com/gaearon/a25fd42a1e6b4cc24851978df0a36571
- Beneath Classes: Prototypes
- https://2ality.com/2015/09/proto-es6.html
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
- https://esdiscuss.org/topic/having-a-non-enumerable-array-prototype-contains-may-not-be-web-compatible