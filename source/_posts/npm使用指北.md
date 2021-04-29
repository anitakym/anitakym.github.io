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