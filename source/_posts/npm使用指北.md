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



