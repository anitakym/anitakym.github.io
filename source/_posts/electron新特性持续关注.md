---
title: electron新特性持续关注
date: 2021-06-16 18:19:21
tags:
---
Electron13新特性

## 基本架构
### chromium-runtime
- Browser Process - 一个
- Renderer Process - 一个或多个

### electron
- Main Process - 增加了nodejs-runtime
- Renderer Process

- IPC通信（和Renderer Process）
- electron API



## 竞品
- https://tauri.app/v1/guides/ - Rust

### electron-to-chromium
- This repository provides a mapping of Electron versions to the Chromium version that it uses.
- 提供version Mapping
- https://www.npmjs.com/package/electron-to-chromium


### carlo
- https://github.com/GoogleChromeLabs/carlo
- 一个思路
- Web rendering surface for Node applications
- 不过已经不再maintain了


### electron-modules
- 一些实用的 Electron 模块
- https://github.com/electron-modules

### electron安装问题
- .npmrc 
- electron_mirror=https://npm.taobao.org/mirrors/electron/
- nrm 设置为https://registry.npm.taobao.org/

现在安装的话，地址都会变成https://registry.npmmirror.com/binary.html?path=electron/
(用CNPM/淘宝源的开发者们请注意，淘宝NPM 镜像站喊你切换新域名啦。新的Web 站点：https://npmmirror.com，Registry Endpoint：https://registry.npmmirror.com。随着新的域名已经正式启用，老 http://npm.taobao.org 和 http://registry.npm.taobao.org 域名将于 2022 年 05 月 31 日零时起停止服务。 )