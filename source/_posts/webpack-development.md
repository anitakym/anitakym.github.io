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

### HardSourceWebpackPlugin
4里面可以用来优化
5里面直接放进去了