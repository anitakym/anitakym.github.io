---
title: nodejs-doc
date: 2021-03-04 12:12:00
tags:
    - node
---

### centos 安装
- rpm
- yum (install | clean all) 如果版本安装有问题，记得按照官方distribution的文档里面写的，做好处理，不然会被缓存影响
- 或者直接通过nvm安装 - https://github.com/nvm-sh/nvm/tree/v0.39.3
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
- centos7不支持nodejs18的安装，会提示依赖有问题，具体可见github上面的issue
```
机器版本：
CentOS Linux release 7.9.2009 (Core)
用户issue：
https://github.com/nodejs/node/issues/43246
官方支持声明：
Supported CentOS versions:
* CentOS 7 (64-bit) WARNING: BUILD SYSTEM CURRENTLY BROKEN FOR NODEJS 18+
* CentOS 8 (64-bit)
* CentOS 8 Stream (64-bit)

因已知及潜在兼容性问题，和官方支持声明，所以安装16+版本，提供nvm进行切换

安装：
走rpm装18的时候的报错

curl -fsSL https://rpm.nodesource.com/setup_lts.x | bash -
Error: Package: 2:nodejs-18.14.2-1nodesource.x86_64 (nodesource)
           Requires: libstdc++.so.6(GLIBCXX_3.4.21)(64bit)
Error: Package: 2:nodejs-18.14.2-1nodesource.x86_64 (nodesource)
           Requires: libm.so.6(GLIBC_2.27)(64bit)
Error: Package: 2:nodejs-18.14.2-1nodesource.x86_64 (nodesource)
           Requires: libstdc++.so.6(GLIBCXX_3.4.20)(64bit)
Error: Package: 2:nodejs-18.14.2-1nodesource.x86_64 (nodesource)
           Requires: libstdc++.so.6(CXXABI_1.3.9)(64bit)
Error: Package: 2:nodejs-18.14.2-1nodesource.x86_64 (nodesource)
           Requires: libc.so.6(GLIBC_2.28)(64bit)
 You could try using --skip-broken to work around the problem
 You could try running: rpm -Va --nofiles --nodigest
```



## latest
- corepack - https://github.com/nodejs/corepack
- undici WG - https://github.com/nodejs/undici
- diagnostics WG - 门槛更低的诊断能力
- Node-API WG - 现代化，API稳定的Addon API
- strategic-initiatives - https://github.com/nodejs/node/blob/main/doc/contributing/strategic-initiatives.md
- https://nodejs.org/calendar
## nodejs-path
### 文档指北：
https://nodejs.org/api/path.html#path_path
http://nodejs.cn/api/path.html
还是推荐dash,可以快速搜索，然后选择右上角copy online page

### 项目经验
node服务项目
electron项目

### globals
- https://nodejs.org/api/globals.html

### Module
- https://nodejs.org/api/packages.html



### querystring
- https://nodejs.org/dist/latest-v16.x/docs/api/querystring.html
```
/**
 * The `querystring` module provides utilities for parsing and formatting URL
 * query strings. It can be accessed using:
 *
 * ```js
 * const querystring = require('querystring');
 * ```
 *
 * The `querystring` API is considered Legacy. While it is still maintained,
 * new code should use the `URLSearchParams` API instead.
 * @deprecated Legacy
 * @see [source](https://github.com/nodejs/node/blob/v18.0.0/lib/querystring.js)
 */
```
- https://nodejs.org/dist/latest-v16.x/docs/api/url.html#class-urlsearchparams

### 基础架构（原理）


### api
#### vm
- https://nodejs.org/api/vm.html
- https://www.youtube.com/watch?v=u81pS05W1JY
- https://pwnisher.gitlab.io/nodejs/sandbox/2019/02/21/sandboxing-nodejs-is-hard.html
用这个实现基于ES6模版字符串语法语法的模版引擎
- 通过VM模块编译JS形成函数
    - include子模版
    - XSS过滤、模版helper函数

### npm
#### easy_sock


#### https://www.npmjs.com/package/protocol-buffers

### slides - ryan dahl 的一系列在conf里面的演讲，不同阶段，可以去YTB上面看
- nodejs ry@tinyclouds 2009 - 最初的设计，为什么这么设计
- https://www.slideshare.net/JSFestUA/js-fest-2019-ryan-dahl-deno-a-new-way-to-javascript

#### perf_hooks
perf_hooks
解决这个报warining的问题
先新建一个项目，引入perf_hooks,没有任何问题
看了不同版本的代码，发现引入的问题，升级了版本即可
http://nodejs.cn/api/perf_hooks.html


### cases
#### fetch - 和nodejs的版本相关
RequestInit: duplex option is required when sending a body #46221
https://github.com/nodejs/node/issues/46221


### addon
Node.js 的 addon 允许本地（C/C++）库与 JavaScript 代码进行交互。这样，JavaScript 不仅能够拥有优秀的编程灵活性，还能在需要的时候利用本地库提高性能。以下是一些使用 Node.js addon 的案例：

图像处理
有些高效的图像处理库是用 C 或 C++ 编写的，如 OpenCV（Open Source Computer Vision Library）。通过使用 addon，这些库可以轻松地与 JavaScript 代码集成，开发出功能强大的 Web 应用程序。例如，可以使用 OpenCV 进行实时视频处理、人脸识别和物体追踪等高性能操作。

加密和解密
加密和解密通常需要执行大量计算，本地库（如 OpenSSL）在这方面的执行效果通常比纯 JavaScript 更高效。Node.js addon 可让我们在 JavaScript 中使用这些本地库，以此来提高加密和解密操作的性能。

文件系统操作
虽然 Node.js 自带了用于文件系统操作的原生模块，但某些特定操作可能需要使用本地库。例如，进行文件压缩与解压缩操作时，本地库（如 zlib）的性能可能优于纯 JavaScript 实现。通过 addon，可以将这些库与 JavaScript 代码相结合，提高应用程序的性能。

数值计算与科学计算
有些数值计算与科学计算库（如 LAPACK - Linear Algebra PACKage、FFTW - Fastest Fourier Transform in the West）是用 C 或 Fortran 编写的，性能优于纯 JavaScript 实现。通过 Node.js addon，可以让这些本地库在 JavaScript 中调用，提高数值计算与科学计算任务的执行效率。

机器学习、深度学习及人工智能
许多高性能机器学习和深度学习库（如 TensorFlow）使用 C++ 或其他本地语言编写。Node.js addon 可以让这些库在 JavaScript 中调用，使我们可以使用 JavaScript 构建高性能的机器学习和深度学习应用程序。