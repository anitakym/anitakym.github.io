---
title: nestjs-design-pattern-summary
date: 2023-06-15 17:44:19
tags:
---
### adapter








### builder





## doc
- 哲学 - 提供了应用程序“架构”
- 安装（$ npm i --save @nestjs/core @nestjs/common rxjs reflect-metadata - 核心和支持文件）
```
rxjs - A reactive programming library for JavaScript - Reactive Extensions Library for JavaScript
RxJS 是一个使用 Observables 进行反应式编程的库，可让异步或基于回调的代码更容易编写。
```
```
reflect-metadata是一个用于装饰器的元数据反射API。这是一种在Javascript中实现元数据反射操作的工具，可以用于增强对象和函数等的功能。
1. 安装导入
   npm i reflect-metadata
   import 'reflect-metadata';
2. 使用装饰器：装饰器可以使用元数据来改进类、属性、方法等
   @Reflect.metadata(metadataKey, metadataValue)
   class MyClass {
   }
3. 查询元数据：
   let data = Reflect.getMetadata(metadataKey, target);
   let ownData = Reflect.getOwnMetadata(metadataKey, target);
4. 避免全局污染：`reflect-metadata`库会污染全局环境，因此应该只在你的应用或库的主要入口点导入一次。它不应该被导入到内部模块中。
5. 配置TypeScript：要在TypeScript中使用元数据反射，你需要在tsconfig.json文件中启用`emitDecoratorMetadata`和`experimentalDecorators`选项。
   {
       "compilerOptions": {
           "target": "ES5",
           "module": "commonjs",
           "experimentalDecorators": true,
           "emitDecoratorMetadata": true
       }
   }
6. 明确元数据键：应该使用Symbol而不是字符串作为元数据键，以避免冲突。
7. 测试：使用`reflect-metadata`时应确保进行适当的单元测试，在大型项目上可以考虑用Mock来模拟这些元数据
```