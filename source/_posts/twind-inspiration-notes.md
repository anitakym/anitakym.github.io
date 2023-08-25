---
title: twind-inspiration-notes
date: 2023-05-22 11:37:15
tags:
---
- https://twind.style/
```
Inspiration
It would be untrue to suggest that the design here is totally original. Other than the founders' initial attempts at implementing such a module (oceanwind and beamwind) we are truly standing on the shoulders of giants.

Tailwind: created a wonderfully thought out API on which the compiler's grammar was defined.
styled-components: implemented and popularized the advantages of doing CSS-in-JS.
htm: a JSX compiler that proved there is merit in doing runtime compilation of DSLs like JSX.
goober: an impossibly small yet efficient CSS-in-JS implementation that defines critical module features.
otion: the first CSS-in-JS solution specifically oriented around handling CSS in an atomic fashion.
clsx: a tiny utility for constructing class name strings conditionally.
style-vendorizer: essential CSS prefixing helpers in less than 1KB of JavaScript.
UnoCSS: for the configuration syntax.
CSSType: providing autocompletion and type checking for CSS properties and values.
```
文档里面有一段inspiration，列举了参考的设计
- Tailwind：创造了一个经过深思熟虑的API，在此基础上定义了编译器的语法。
- styled-components：实现并推广了在JS中使用CSS的优势。
- htm：一个JSX编译器，证明了对DSL（如JSX）进行运行时编译的好处。
- goober：一个小得不能再小但高效的CSS-in-JS实现，定义了关键的模块特性。
- otion：第一个CSS-in-JS解决方案，专门用于以原子方式处理CSS。
- clsx：一个用于有条件地构建类名字符串的小工具。
- style-vendorizer：在不到1KB的JavaScript中提供基本的CSS前缀辅助工具。
- UnoCSS：用于配置语法。
- CSSType：为CSS属性和值提供自动补全和类型检查。



### windi css
- Windi CSS is a next-generation utility-first CSS framework.
- 为什么选择 Windi CSS？
作者的一段话应能说明他创建 Windi CSS 的动机：
当我的项目变得越来越大，有大约几十个组件时，初始编译时间达到了 3 秒，而使用 Tailwind CSS 进行热更新则需要 1 秒以上。- @voorjaar
通过扫描 HTML 和 CSS 并按需生成实用程序，Windi CSS 能够在开发过程中提供更快的加载时间和更快的 HMR，而在生产过程中则无需清除。