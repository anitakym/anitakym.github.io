---
title: metadata-reflection-summary
date: 2023-12-28 14:33:54
tags:
---
Metadata Reflection API 是 TypeScript 提供的一种机制，它允许在运行时访问类、接口或者类型的元数据。这对于某些开发工作，如装饰器、DI框架（依赖注入框架）、对象映射等，非常有帮助。

这个 API 采用于 ECMAScript 的装饰器提案，它有以下三个主要的部分：

1. Reflect.metadata：用于添加指定的元数据到类的定义上。
2. Reflect.defineMetadata：用于在一个对象上定义新的元数据。
3. Reflect.getMetadata：用于获取已定义的元数据。

要使用这个 API，你需要在 tsconfig.json 文件里，把 "emitDecoratorMetadata" 设置为 true。

以下是一个例子，演示了如何使用 Metadata Reflection API：

```ts
// 定义一个装饰器
function logType(target : any, key : string) {
  let t = Reflect.getMetadata("design:type", target, key);
  console.log(`${key} type: ${t.name}`);
}

class Demo {
  @logType // 应用装饰器
  public attr1 : string;
}

// 输出：attr1 type: String
```

在这个例子中，"logType" 装饰器使用了 Reflect.getMetadata 函数来取得 "attr1" 的类型，然后输出的结果就是 "attr1 type: String"。

总的来说，Metadata Reflection API 提供了在运行时访问类型信息的功能，这使得 TypeScript 在很多场景下更具灵活性和强大的动态编程能力。


这段话的意思是，现在Decorators和Decorator Metadata已经在TC39中达到了第三阶段，以下提出的API不再被考虑作为标准化。然而，这个包将继续支持那些利用TypeScript的遗留--experimentalDecorators选项的项目，因为一些项目可能无法迁移到使用标准的装饰器。

TC39是JavaScript标准化组织。它通过阶段（共4个阶段）对JavaScript的特性进行标准化讨论。需要注意的是，达到第三阶段，表示该特性已经接近最终确定并将在未来的版本中作为标准特性出现。

这个段落是告诉你，虽然Decorator和Decorator Metadata已经基本确定为标准特性，但是在这个包中还将继续支持TypeScript早期的—experimentalDecorators选项，以保证后向兼容性，并且方便那些还使用旧版TypeScript的项目。

### Decorators
- https://www.typescriptlang.org/docs/handbook/decorators.html
NOTE  This document refers to an experimental stage 2 decorators implementation. Stage 3 decorator support is available since Typescript 5.0. See: Decorators in Typescript 5.0

- https://devblogs.microsoft.com/typescript/announcing-typescript-5-0/#decorators