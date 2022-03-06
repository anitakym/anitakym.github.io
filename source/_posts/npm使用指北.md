---
title: npm使用指北
date: 2021-03-17 14:48:34
tags:
---

查看全局安装的包的版本
```
npm list -g --depth 0 | grep @vue/cli
```

### 问题处理
(node:50731) ExperimentalWarning: Package name self resolution is an experimental feature. This feature could change at any time
94% after seal[hardsource:a9cf9509] Could not freeze ./src/router/index.js: Cannot read property 'hash' of undefined
98% after emitting

### error
```
UNMET PEER DEPENDENCY webpack@4.x.x || 5.x.x

npm ERR! peer dep missing: webpack@4.x.x || 5.x.x, required by webpack-cli@4.9.2
npm ERR! peer dep missing: webpack@4.x.x || 5.x.x, required by @webpack-cli/configtest@1.1.1
npm ERR! extraneous: which@2.0.2 /Users/xxxxx/node_modules/cross-spawn/node_modules/which
```
#### peer dep
- https://blog.domenic.me/peer-dependencies/

### n
n升级到lts的时候出了问题

node -v
dyld: initializer function 0x0 not in mapped image for /usr/local/bin/node

brew uninstall --force node
brew uninstall icu4c && brew install icu4c
brew unlink icu4c && brew link icu4c --force
brew install node

I recently encountered a similar issue (after doing brew switch node 9.8.0 to downgrade to a previous version of node)

dyld: Library not loaded: 
/usr/local/opt/icu4c/lib/libicui18n.60.dylib
  Referenced from: /usr/local/bin/node
  Reason: image not found
Abort trap: 6
The issue is that node is picky about which version of icu4c it's looking for, and the version I had installed (62) was higher than node was expecting.

To fix, I made sure I had version 60 of icu4c selected.

First I found which versions I had with brew info icu4c, then did brew switch icu4c 60.2 to select the one node was expecting.

重新官网下载了node,解决的
https://nodejs.org/en/

### npx
可以通过npx,去执行cli命令，不需要额外的安装
比如：
```
npx create-next-app test-demo
npx create-react-app test-app
(If you've previously installed create-react-app globally via npm install -g create-react-app, we recommend you uninstall the package using npm uninstall -g create-react-app or yarn global remove create-react-app to ensure that npx always uses the latest version.)
```
npx主要用于命令行寻址等辅助功能上

### yarn
可以通过homebrew安装，也可以通过npm安装
https://yarnpkg.com/getting-started
yarn autoclean 功能可以试试

https://gist.github.com/jonlabelle/c082700c1c249d986faecbd5abf7d65b
https://shift.infinite.red/npm-vs-yarn-cheat-sheet-8755b092e5cc
这篇文章提供npm和yarn的对比：
官方也有简单的vs：
https://classic.yarnpkg.com/en/docs/migrating-from-npm
```
npm install === yarn
npm installl testpackage --save === yarn add testpackage
npm uninstall testpackage --save === yarn remove testpackage
npm install testpackage --save-dev === yarn add testpackage --dev
npm update --save === yarn upgrade
```
```
// 都一样的
init | link | outdated | publish | run | cache clean | login | test
```
```
// yarn 有npm没有的
yarn licenses list
yarn why lodash
```

### node_modules/.bin
```
通过npm启动的脚本，会默认把node_modules/.bin加到PATH环境变量中
https://docs.npmjs.com/cli/v7/commands/npm-run-script

当某个模块配置了 bin 定义时，就会被安装的时候，自动软链了过去
https://docs.npmjs.com/cli/v7/configuring-npm/package-json/#bin
```

### .npmrc
可以先看下```npm config ls -l```
https://docs.npmjs.com/cli/v7/configuring-npm/npmrc
<pre>
具体项目：
registry 可以在这个里面设置

可以设置
package-lock=false
koa就是这么设置的
// 说明:如果设置为false，那么在安装时将忽略package-lock.json文件
package-lock
Default: true
Type: Boolean
If set to false, then ignore package-lock.json files when installing. This will also prevent writing package-lock.json if save is true.

When package package-locks are disabled, automatic pruning of extraneous modules will also be disabled. To remove extraneous modules with package-locks disabled use npm prune.
</pre>

### pnpm
- https://pnpm.io/zh/motivation
- pnpm - 依赖项将存储在一个内容可寻址的仓库中
- npm - 依赖都会被提升到模块的根目录 - 扁平化结构
- pnpm - 使用软链的方式将项目的直接依赖添加进模块文件夹的根目录。 
```
树形的问题：
This approach had two serious issues:
- frequently packages were creating too deep dependency trees, which caused long directory paths issue on Windows
- packages were copy pasted several times when they were required in different dependencies
To solve these issues, npm rethought the node_modules structure and came up with flattening. 
```
- 推荐阅读：https://www.kochan.io/ 这个里面写了几篇文章
- vue-next用pnpm,还在preinstall里面加了验证
- vite - only allow pnpm

### difference
- https://mp.weixin.qq.com/s?__biz=Mzg4MTYwMzY1Mw==&mid=2247496601&idx=1&sn=4c3bc00c37163e1dca152ebb8f723619&source=41#wechat_redirect

## 项目管理
### init
- ```npm init```

### package.json
见```谈一谈package-json文件```博文