---
title: CMake
date: 2021-06-21 15:58:20
tags:
---
### 官方文档
CMake is an open-source, cross-platform family of tools designed to build, test and package software. 

CMake is used to control the software compilation process using simple platform and compiler independent configuration files, and generate native makefiles and workspaces that can be used in the compiler environment of your choice. 

The suite of CMake tools were created by Kitware in response to the need for a powerful, cross-platform build environment for open-source projects such as ITK and VTK.

CMake is part of Kitware’s collection of commercially supported open-source platforms for software development.

### 学习参考文档
https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1

https://github.com/ttroy50/cmake-examples

### 实例：
https://github.com/openkraken/kraken

Prerequisites

Node.js v12.0 or later
Flutter version in the kraken/pubspec.yaml
CMake v3.2.0 or later
Xcode (10.12) or later (Running on macOS or iOS)
Android NDK version 21.4.7075529 (Running on Android)

### harmonyOS已知问题
- 如果makefile中的业务逻辑存在并发操作，由于CMake机制上通过多线程执行，在多CPU架构并发操作场景，会偶现编译失败。规避措施：建议排查并修改makefile中的业务逻辑，去除并发操作。
- https://developer.harmonyos.com/cn/docs/documentation/doc-releases-V3/ide-known-issues-v3-1-0000001440852961-V3