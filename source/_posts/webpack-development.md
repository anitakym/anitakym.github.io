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
https://webpack.docschina.org/guides/build-performance/

worker 池(worker pool) 
thread-loader 可以将非常消耗资源的 loader 分流给一个 worker pool。

Warning
不要使用太多的 worker，因为 Node.js 的 runtime 和 loader 都有启动开销。最小化 worker 和 main process(主进程) 之间的模块传输。进程间通讯(IPC, inter process communication)是非常消耗资源的。
需要谨慎使用～


### chokidar
- https://www.npmjs.com/package/chokidar
- Minimal and efficient cross-platform file watching library
- webpack-dev-server 的依赖
- 比如说这个博客，基于hexo,hexo-fs也依赖chokidar

### webpack-cli
#### 命令行工具cli
- 可以在处理node时候，模块这部分，命令行编译
- npx webpack [command] [options]
- 可以免安装
- 注意webpack版本和对应的用法
- ```npx webpack --no-devtool --mode development --target node14.5```