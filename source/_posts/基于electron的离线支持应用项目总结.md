---
title: 基于electron的离线支持应用项目总结
date: 2021-11-09 18:07:30
tags:
---
### history
> 一个15年的应用，之所以支持离线，是因为校区教室内的网络可能不好，所以需要课中使用时支持离线；

- 那个时候electron的版本和相关构建生态都是比较开始的阶段，基于node的版本也比较低，过了几年，重新起那个项目

```
npm run start
(会发生fse.node无法通过安全与偏好设置，这个需要在安全与偏好设置里面同意一下)

开始错误暂不影响看，可点过掉


● electron-mocha
- https://mochajs.org/
- https://github.com/mochajs/mocha

● electron-prebuilt
  ○ npm地址： https://www.npmjs.com/package/electron-prebuilt
  ○ 说明：electron-prebuilt has been renamed to electron. For more details, see http://electron.atom.io/blog/2016/08/16/npm-install-electron

```
"requires": {
        "electron-download": "^3.0.1",
        "extract-zip": "^1.0.3"
      }
```
被重新命名为electron了（https://www.electronjs.org/blog/npm-install-electron）

● Mac，Windows包(利用两个工具，流程化得进行封包工作)
  ○ appdmg
  ○ rcedit

(基于seal_electron)
● 测试模块
https://www.electronjs.org/spectron
● 构建模块
dps:
electron-log
electron-updater

dev-deps:
electron
electron-builder
electron-webpack
```

### 截屏功能



### electron rebuild
This executable rebuilds native Node.js modules against the version of Node.js that your Electron project is using. This allows you to use native Node.js modules in Electron apps without your system version of Node.js matching exactly (which is often not the case, and sometimes not even possible).
该可执行文件将根据您的Electron项目使用的Node.js版本重建本机Node.js模块。这使您可以在Electron应用程序中使用本机Node.js模块，而无需与系统版本的Node.js完全匹配
- 可配置到script中

### Arch

#### 主进程
- browser window（浏览器窗口，加载网页，注入JSSDK，挂window上面）
- electron updater （客户端更新）
- 客户端监控 - sentry

#### 渲染进程
- JSSDK （暴露给嵌入的页面）


### 功能模块
#### 文件下载
- 网页向客户端提出下载的请求
- 客户端提供了下载的功能，由客户端向服务的请求数据，完成下载，并回调给网页进度和状态
- https://www.electronjs.org/docs/latest/tutorial/process-model#preload-scripts
- JSSDK的注入是通过preload scripts


### 网页端
- babel 是可以配置 electron兼容的
- https://babeljs.io/docs/en/options#targets
"@babel/preset-env",
      {
        "targets": {
          "electron": "9",
        }
      }



## sentry 

#### EXCEPTION_ACCESS_VIOLATION_READ
https://source.chromium.org/chromium#chromium/src/v8/src/deoptimizer.cc&sq=package:chromium&l=680
https://github.com/electron/electron/issues/3241


### 其他产品
- 语雀的客户端(https://www.yuque.com/download)
- https://www.yuque.com/seeconf/2022/kr8mdw  - 开发的分享 - 如何打造高质量的基于electron的客户端


### electron-builder
electron-builder 自身不对 Python 的版本有直接的要求，因为它是用 JavaScript 编写的。
然而，有些依赖可能需要 Python。例如，一些原生模块可能使用 node-gyp 进行构建，而 node-gyp 需要 Python 2.7（注意不是 Python 3）。
因此，在使用 electron-builder 时，虽然 electron-builder 自身对 Python 的版本没有直接要求，但如果你正在使用的项目中有需要 node-gyp 来构建的模块，那么就需要确保你的环境中安装了 Python 2.7。
不过，如果在构建过程中遇到与 Python 相关的问题，建议检查你的环境设置以及项目的依赖，并确保它们与 Python 的版本兼容。



### level
`leveldown`是一个为LevelDB编写的Node.js模块，LevelDB是谷歌开发的一种快速键值存储系统。`leveldown`充当LevelDB和Node.js之间的接口，使LevelDB的功能可以用JavaScript进行操作。

具体来说，`leveldown`允许数据的存储、查询、删除和更新。它可用于处理大量数据，因为LevelDB设计用于处理高速大容量数据存储。

此包通常与`levelup`包一起使用，`levelup`在`leveldown`之上添加了一些额外的功能，如数据编码和解码，以及读写流。


LevelDB 是 Google 开发的一款高效的键值对存储库，它提供了接口来处理大型数据。LevelDB 使用 log-structured merge-tree（LSM树）数据结构，这样可以提供高速的读和写途径。因此，LevelDB 特别适合于处理大量数据的场景。

一些主要特点包括：

1. 自动数据压缩：LevelDB 使用谷歌的 Snappy 数据压缩库来减少存储占用的空间。

2. 原子批处理：LevelDB 支持“批处理”操作，这样可以保证一系列操作作为一个单元进行，要么全部成功，要么全部失败，这就是所谓的“原子性”。

3. 快速查找：由于 LSM 树的数据结构特性，LevelDB 提供非常快速的键值对查找。

LevelDB 在很多领域有广泛应用，包括网页索引、用户数据存储、缓存等场景。