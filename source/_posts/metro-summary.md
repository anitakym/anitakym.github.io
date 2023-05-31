---
title: metro-summary
date: 2023-05-31 10:01:16
tags:
---

### metro
Metro 是一款由 Facebook 开发的自动化打包器和优化器，用于加速 React Native 和 Node.js 的开发。Metro 不仅在 Facebook 得到了广泛应用，还在其他很多公司和开源项目中使用。一些使用 Metro 的知名案例包括：

Walmart：全球最大的零售商之一，使用 Metro 优化其 React Native 应用程序。
Expo：提供了一个从头开始开发 React Native 应用程序的工具套件，内部使用了 Metro。
Callstack：专门从事 React Native 项目开发的 IT 公司，使用 Metro 作为其优化器和打包器。
Wix：为其 React Native 应用程序使用 Metro 进行打包和优化。
Microsoft: 使用 Metro 作为其 React Native for Windows 和 React Native for macOS 项目的一部分。

- metro提供Javascript的bundler的功能
## 概念
#### 构建阶段 - bundling process
- Resolution：此阶段Metro会从入口文件出发分析所依赖的模块生成一个所有模块的依赖图，主要是使用jest-haste-map这个包做依赖分析。这个阶段和Transformation阶段是并行的；
- Transformation：此阶段主要是将模块代码转换成目标平台可识别的格式；
- Serialization：此阶段主要是将Transform后的模块进行序列化，然后组合这些模块生成一个或多个Bundle

### cases
#### React Native工程Monorepo改造实践
- https://juejin.cn/post/7177585131861835837
#### 基于 React Native 的动态列表方案探索
- https://juejin.cn/post/7142819695840722975


## deep dives
里面四个点可以看看
#### bundle formats
#### caching
#### module resolution
#### source map format