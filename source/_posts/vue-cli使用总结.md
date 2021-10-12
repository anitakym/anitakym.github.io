---
title: vue-cli使用总结
date: 2021-03-17 14:51:05
tags:
---
https://cli.vuejs.org/zh/guide/css.html#%E5%BC%95%E7%94%A8%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90
还是基于webpack的，探索rollup及vite

### Vue Cli 3.0重构原因
from Evan You(https://medium.com/@youyuxi)
(medium.com)
一般vue相关官方发布的时候，Evan You会在medium上面发文章，阐述思想，这部分还是蛮值得看的。存在什么问题，为什么要解决，怎么解决的。

https://medium.com/the-vue-point/vue-cli-3-0-is-here-c42bebe28fbb
```
尤雨溪认为，旧版本的 Vue CLI 本质上只是从 GitHub 上拉取模版，这种拉模版的方式有几个问题：
在单个模版里面同时支持太多选项，会导致模版本身变得极其复杂和难以维护，而提供多个模版一方面会让初学者无所适从，另一方面模版之间也难以共享功能或是互相迁移。

CLI 3 的解决方案是通过插件的形式，去支持多个不同的功能，一个插件对应一个功能，这样就避免了多个模版，也使得 CLI 自身的可维护性得到提升。

拉模版生成的项目，所有的 webpack 配置和构建脚本都直接包含在仓库中，一旦用户对这些部分做了修改，就很难再获得源模版的更新和升级。

CLI 3 生成的项目，核心的 webpack 配置和构建逻辑都被封装在依赖中，同时，允许用户通过配置文件来进行底层的修改。由于核心配置都被封装起来了，所以就有更多的空间去做更复杂的功能和优化，而不用担心用户的项目里面，充斥着大量和应用本身无关的构建代码。

尤雨溪表示，Vue CLI 3.0 中加入了 GUI，主要就是为了降低使用门槛，因为命令行能展示的交互很有限，所以默认用户对于创建项目时，涉及的各种工具和配置项都有了基本的了解。

而 GUI 可以提供更多的信息，帮助用户了解这些东西是干嘛的。

另外，GUI 也能提供一些命令行无法展示的信息，比如，通过可视化的图表分析打包后各个模块的大小占比等。


Vue CLI 的核心目标是为基于 webpack 4 构建的预配置提供构建设置，目标是最大限度地减少开发人员配置的次数，因此，Vue CLI 3 对具有以下特点的项目都支持开箱即用：预配置 webpack 功能，如模块热替换、代码拆分、摇树优化（tree-shaking）、高效持久化缓存等；通过 Babel 插件（Babel 7 + preset-env）对 ES2017 进行转换；支持 PostCSS（默认启用 autoprefixer）和所有主要的 CSS 预处理器；Modern mode：并行发布原生 ES2017 +bundle 和传统 bundle；多页面模式：构建具有多个 HTML / JS 入口点的应用程序；构建目标：将 Vue 单文件组件构建成为库或原生 Web 组件。

Vue CLI 的核心目标是为基于 webpack 4 构建的预配置提供构建设置，目标是最大限度地减少开发人员配置的次数，因此，Vue CLI 3 对具有以下特点的项目都支持开箱即用：预配置 webpack 功能，如模块热替换、代码拆分、摇树优化（tree-shaking）、高效持久化缓存等；通过 Babel 插件（Babel 7 + preset-env）对 ES2017 进行转换；支持 PostCSS（默认启用 autoprefixer）和所有主要的 CSS 预处理器；Modern mode：并行发布原生 ES2017 +bundle 和传统 bundle；多页面模式：构建具有多个 HTML / JS 入口点的应用程序；构建目标：将 Vue 单文件组件构建成为库或原生 Web 组件。

尤雨溪认为，以低级别形式访问 configs 具有很重要的意义，但是他不想抛弃那些“eject”的用户，所以他找出了一种无需 eject 的配置方法。

对于 Babel、TypeScript 和 PostCSS 等第三方集成来说，Vue CLI 会尊重这些工具的配置文件。webpack 用户可以使用 webpack-merge 将简单的对象合并到最终配置中，或通过 webpack-chain 进行精确定位和调整现有的加载器和插件。此外，Vue CLI 附带了 vue inspect 命令，可以帮助开发者检查内部 Webpack 配置。这样做最大的好处是，只需要微小的调整，而不需要 eject，就可以升级 CLI service 和插件进行修复或更新。尤雨溪表示，Vue CLI 3 现在可以作为 Vue 应用程序的标准构建工具，但是这仅仅是个开始，它的长期目标是将当前和未来的最佳实践融入工具链中，最终为用户提供高性能的应用程序。


```

目前npm拉包默认是4.x，5还在发alpha版本(5.0.0-alpha.7 (2021-03-11))



## 相关Tips
@vue/cli 
如果你已经全局安装了旧版本的 vue-cli (1.x 或 2.x)，你需要先通过 npm uninstall vue-cli -g 或 yarn global remove vue-cli 卸载它。
```
vue --version
npm update -g @vue/cli
```

### report
https://cli.vuejs.org/zh/guide/cli-service.html#vue-cli-service-serve
- options 里面有--report