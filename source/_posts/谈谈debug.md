---
title: 谈谈debug
date: 2020-07-06 16:31:04
tags:
    - debug+proxy篇
---


#### vscode中debug
#####  原理说明： vscode把debug功能的实现交付给插件完成的（vscode提供了Debug Adapter Protocol —— DAP）
插件=>把调试和vscode的界面和交互结合
vscode=》用户在界面的操作，vscode通过DAP唤起插件，插件完成最终的操作

文档指路：
https://microsoft.github.io/debug-adapter-protocol/
https://code.visualstudio.com/api/extension-guides/debugger-extension


##### 操作指南
- cmd + shift + D 
- 点击调试按钮，选择环境


#### ndb-firekylin调试
https://zhuanlan.zhihu.com/p/41315709


#### Vue相关问题快速排查之debug

涉及一些Vue本身相关的问题，首先查文档，略微查下源码，能解决的就解决了；还是有疑问的，对相关疑问点进行debug调试


借助vue-cli3：
https://cli.vuejs.org/zh/guide/prototyping.html
快速原型开发
你可以使用 vue serve 和 vue build 命令对单个 *.vue 文件进行快速原型开发，不过这需要先额外安装一个全局的扩展：
npm install -g @vue/cli-service-global
vue serve 的缺点就是它需要安装全局依赖，这使得它在不同机器上的一致性不能得到保证。因此这只适用于快速原型开发。
#
vue serve
Usage: serve [options] [entry]

在开发环境模式下零配置为 .js 或 .vue 文件启动一个服务器


Options:

  -o, --open  打开浏览器
  -c, --copy  将本地 URL 复制到剪切板
  -h, --help  输出用法信息
你所需要的仅仅是一个 App.vue 文件：
<template>
  <h1>Hello!</h1>
</template>
然后在这个 App.vue 文件所在的目录下运行：
vue serve
vue serve 使用了和 vue create 创建的项目相同的默认设置 (webpack、Babel、PostCSS 和 ESLint)。它会在当前目录自动推导入口文件——入口可以是 main.js、index.js、App.vue 或 app.vue 中的一个。你也可以显式地指定入口文件：
vue serve MyComponent.vue
如果需要，你还可以提供一个 index.html、package.json、安装并使用本地依赖、甚至通过相应的配置文件配置 Babel、PostCSS 和 ESLint。


template文件：
开发的ide是vscode,所以可以安装相应的snippets

1.可以有一些插件
2.可以自定义用户snippet（https://code.visualstudio.com/docs/editor/userdefinedsnippets）
 There is also support for tab-completion: Enable it with "editor.tabCompletion": "on", type a snippet prefix (trigger text), and press Tab to insert a snippet.
(可以增加如下配置)

#### node-assert
webpack-debug

DevTools=>Devices=>Target build/build.js


#### ndb
ndb
https://chromedevtools.github.io/devtools-protocol/

#### 平台｜环境｜工具｜方法
- 浏览器，hybrid，nodejs,小程序，electron
- local| online
- chrome devtools | charles | spy-debugger | whistle | vConsole
- console | breakpoint | sourceMap | proxy

## chrome
#### 动态修改样式
- .cls
- computed -> 跳转到styles
- 强制激活伪类 - 选中具有伪类的元素 点击:hov
- 强制激活伪类 - DOM树右键菜单，选择Force State
#### console
- .table 和 .dir 可根据场景，选择打印，方便观察
- %d %o %s %c 占位符- 字符串替换 - 增加样式，格式

#### sourcemap
- mappings => 映射 https://www.murzwin.com/base64vlq.html

#### performance
- frames帧线程
- main主线程，JS执行｜html/css解析，完成绘制
- raster 完成某个layer或者tile的绘制
- https://googlechrome.github.io/devtools-samples/jank/
- FPS | CPU | NET - 概览分析，看性能节点

#### lighthouse
- LCP - 加载性能
- FID - 交互性
- CLS - 视觉稳定性