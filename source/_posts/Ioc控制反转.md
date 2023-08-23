---
title: Ioc控制反转
date: 2022-09-27 16:44:09
tags:
---
- https://medium.com/nmc-techblog/dip-ioc-di-know-them-better-abed5b57fd20
- https://martinfowler.com/articles/injection.html

```
面向对象编程 - 设计原则
控制反转（Inversion of Control，缩写为 IoC）
降低代码之间的耦合度

方式
依赖注入（Dependency Injection）
依赖查找（Dependency Lookup）

通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体将其所依赖的对象的引用传递给它
依赖被注入到对象中
```


1. InversifyJS：是一个强大且轻量的反转控制(IoC)容器，用于JavaScript和Node.js的开发，支持TypeScript。它使用了类似于Java的注解方式引入依赖，让开发者更专注于业务代码的开发。

2. tsyringe：是一个轻量级的依赖注入容器，有着简洁易懂的API和易于操作的使用方式，也共享了类似Hilt的理念。它支持构造函数注入、属性注入和方法注入，大大方便了开发过程。

3. NestJS：虽然它主要是一个Node.js后端开发框架，但其中内嵌了一套依赖注入系统。这个系统虽然简单，但非常灵活，可以帮助你管理项目中的各种服务和组件。

4. TypeDI: 这也是一个强大的IoC容器库。它能和TypeORM，routing-controllers等库无缝集成，为开发者提供一套完整的开发解决方案。

## nestjs
- 实现了 IOC 容器
- 从入口模块开始扫描
- 分析 Module 之间的引用关系，对象之间的依赖关系
- 自动把 provider 注入到目标对象

- provider 一般都是用 @Injectable 修饰的 class
- 构造器注入: 通过 provide 指定注入的 token，通过 useClass 指定注入的对象的类，Nest 会自动对它做实例化再注入
- 属性注入: 通过 @Inject 指定注入的 provider 的 token
- vs: 用 class 做 token 可以省去 @Inject
- provider 的值可能是动态产生的，Nest 也同样支持(用 useFactory 来动态创建一个对象,useFactory 也支持参数的注入，支持异步)