---
title: webpack-development
date: 2020-11-19 18:44:52
tags:
    - webpack
---
#### webpack-dev-server
webpack-dev-server是一个小型的Node.js Express服务器,它使用webpack-dev-middleware来服务于webpack的包,除此自外，它还有一个通过Sock.js来连接到服务器的微型运行时.

sock.js(https://github.com/sockjs/sockjs-client):



### alias




### sass-loader
https://github.com/webpack-contrib/sass-loader#imports 
<pre>
Using ~ is deprecated and can be removed from your code (we recommend it), but we still support it for historical reasons. Why you can remove it? The loader will first try to resolve @import as relative, if it cannot be resolved, the loader will try to resolve @import inside node_modules. Just prepend them with a ~ which tells webpack to look up the modules.

@import "~bootstrap";
It's important to only prepend it with ~, because ~/ resolves to the home directory. Webpack needs to distinguish between bootstrap and ~bootstrap because CSS and Sass files have no special syntax for importing relative files. Writing @import "style.scss" is the same as @import "./style.scss";


</pre>

旧的版本，如果不加 ～
Module build failed (from ./node_modules/sass-loader/lib/loader.js):

undefined
 ^
      File to import not found or unreadable: @/views/plan/publish/publish.scss.

issues:
https://github.com/teambit/bit/issues/1103

<pre>
webpack provides an advanced mechanism to resolve files. The sass-loader uses Sass's custom importer feature to pass all queries to the webpack resolving engine. Thus you can import your Sass modules from node_modules. Just prepend them with a ~ to tell webpack that this is not a relative import:

@import "~bootstrap/dist/css/bootstrap";
It's important to only prepend it with ~, because ~/ resolves to the home directory. webpack needs to distinguish between bootstrap and ~bootstrap because CSS and Sass files have no special syntax for importing relative files. Writing @import "file" is the same as @import "./file";

</pre>

### HardSourceWebpackPlugin
4里面可以用来优化
5里面直接放进去了

现有问题：
https://github.com/mzgoddard/hard-source-webpack-plugin/issues/416


### 构建性能优化
#### official - doc
- https://webpack.docschina.org/guides/build-performance/

> 将 Node.js 更新到最新版本，也有助于提高性能。除此之外，将你的 package 管理工具（例如 npm 或者 yarn）更新到最新版本，也有助于提高性能。较新的版本能够建立更高效的模块树以及提高解析速度。 - doc
- loader | bootstrap | 解析 ｜ dll | smaller = faster | worker pool | 持久化缓存 ｜ 自定义的plugin和loader分析

#### Warning
- worker 池(worker pool) 
- thread-loader 可以将非常消耗资源的 loader 分流给一个 worker pool。

- 不要使用太多的 worker，因为 Node.js 的 runtime 和 loader 都有启动开销。最小化 worker 和 main process(主进程) 之间的模块传输。进程间通讯(IPC, inter process communication)是非常消耗资源的。需要谨慎使用～

#### 通用 ｜ 开发 ｜生产
- 不同环境的优化

#### reference
- http://webpack.wuhaolin.cn/4%E4%BC%98%E5%8C%96/
### chokidar
- https://www.npmjs.com/package/chokidar
- Minimal and efficient cross-platform file watching library
- webpack-dev-server 的依赖
- 比如说这个博客，基于hexo,hexo-fs也依赖chokidar
- chokidar中有个依赖-fsevents

### webpack-cli
#### 命令行工具cli
- 可以在处理node时候，模块这部分，命令行编译
- npx webpack [command] [options]
- 可以免安装
- 注意webpack版本和对应的用法
- ```npx webpack --no-devtool --mode development --target node14.5```


## build process - JavaScript Bundler
#### Rollup
- https://github.com/rollup/rollup
- https://rollupjs.org/guide/en/#tools - 和其他工具的集成
#### microbundle
#### snowpack
#### Parcel
- 简单好用


## source
- https://docs.google.com/presentation/d/1hFtMCMo62DgOIc-9OwgaVwPZHwv1cgMELArHcMbXlSI
- https://github.com/thelarkinn/webpack-workshop-2018

## create-react-app
### after eject
#### lint
```
Parsing error: [BABEL] /Users/kuangyimin/Documents/公司/新东方/进行项目/yy/react-playground/scripts/build.js: Using `babel-preset-react-app` requires that you specify `NODE_ENV` or `BABEL_ENV` environment variables. Valid values are "development", "test", and "production". Instead, received: undefined.

所以需要指定下
NODE_ENV=development BABEL_ENV=development eslint . --ext .js,.jsx,.ts,.tsx src
```


#### test
    "test": "node scripts/test.js",
- 注意node版本
```
因为test的原因，node版本需要大于14.17.0
不然
```
 import { PatternPrompt, printPatternCaret, printRestoredPatternCaret } from 'jest-watcher';
                            ^^^^^^^^^^^^^^^^^
    SyntaxError: Named export 'printPatternCaret' not found. The requested module 'jest-watcher' is a CommonJS module, which may not support all module.exports as named exports.
    CommonJS modules can always be imported via the default export, for example using:

    import pkg from 'jest-watcher';
    const { PatternPrompt, printPatternCaret, printRestoredPatternCaret } = pkg;
```
- https://github.com/facebook/create-react-app/issues/11792

```
#### less
- github.com/DocSpring/craco-less


#### better-scripts
```
Executing script: build_diy

to be executed: react-app-rewired build 
false process.argv.includes('--analyze')
当前环境为生产环境
Creating an optimized production build...

  `@babel/polyfill` is deprecated. Please, use required parts of `core-js`
  and `regenerator-runtime/runtime` separately

Treating warnings as errors because process.env.CI = true.
Most CI servers set it automatically.

Failed to compile.

src/component-diy/layout/index.js
  Line 9:1:  `@/component/QuestionTools` import should occur after import of `api/ajax-project`  import/order

src/component/QuestionTools/components/SingleQuestion/index.js
  Line 213:8:  JSX props should not use functions  react/jsx-no-bind
  Line 231:8:  JSX props should not use functions  react/jsx-no-bind

src/component/QuestionTypes/GapFillingQuestion/index.js
  Line 87:5:  JSX props should not use functions  react/jsx-no-bind
  Line 97:6:  JSX props should not use functions  react/jsx-no-bind


npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! seal_react_backend_new@0.1.0 build:diy: `better-npm-run build_diy`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the seal_react_backend_new@0.1.0 build:diy script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
```
```
"build_prod": {
      "command": "CI=false&&react-app-rewired build",
      "env": {
        "REACT_APP_BUILD_TYPE": "online"
      }
    },
```
CI设置为false，避免把warning当成error处理，导致构建直接退出

#### lint需要再配置

#### mini-css-extract-plugin Conflicting order
- 分离并打包CSS到单独文件
- https://github.com/webpack-contrib/mini-css-extract-plugin/issues/250
- https://stackoverflow.com/questions/51971857/mini-css-extract-plugin-warning-in-chunk-chunkname-mini-css-extract-plugin-con/67579319#67579319

## 基础

