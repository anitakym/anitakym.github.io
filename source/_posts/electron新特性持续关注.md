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