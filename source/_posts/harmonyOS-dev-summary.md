---
title: harmonyOS-dev-summary
date: 2023-08-15 15:25:59
tags:
---
- 真机测试
- hdc 如果报inner error，先要确认真机的API版本，然后再进行开发

## 开发模型
- FA（不建议使用）
- Stage（1.支持多窗口2.进程单ArkTS引擎）

进程间的数据和内存共享是操作系统中一个重要的概念，特别是在多任务和并发编程中。如果一个引擎运行在单一进程上，并且所有应用程序也在这同一进程中运行，它们将能够直接访问相同的内存空间，实现无缝的数据共享。

这种设计可以提高数据访问的效率，因为它消除了进程间通信（IPC）的需要，而进程间通信至少需要一次上下文切换和数据拷贝，这对性能的影响是很大的。另一方面，这种设计也会带来一些挑战，比如应用程序之间的隔离性和安全性问题，因为在同一进程中运行的应用程序理论上能够访问进程的所有资源。

## HAP
- 一个可以独立运行的完整模块
- like - aab标准包格式
- 华为HAP (HarmonyOS Ability Package) 是华为为其操作系统 HarmonyOS 设计的一种应用程序包格式。为了在 HarmonyOS 设备上运行，应用程序需要被打包为 HAP 包。
以 HAP 格式打包的应用程序可以在多种类型的 HarmonyOS 设备上运行，包括智能手机、智能电视、智能穿戴装置等。
HAP 包包含应用程序的所有资源，包括代码、静态文件、图标等。它们可以从华为的分发平台（如 AppGallery）上下载并安装。
- 相同能力内敛+按需加载，共享能力减少包体积大小

## ohpm
- 基于npm,pnpm


## HAR/HSP
- 在app中是否以单例模式存在
- har,在不同的模块，存在不同的包实例
- hsp,模块的包实例是同一个

## 组件和状态
UI描述
数据与数据状态交互处理（底层逻辑）

ArkUI - 声明式表达UI
ArkTS - ArkTS 是 HarmonyOS 优选的主力应用开发语言。ArkTS 围绕应用开发在 TypeScript（简称 TS）生态基础上做了进一步扩展，继承了 TS 的所有特性，是 TS 的超集。 

```
1.Basic Setup
execute install task, component ohpm.zip.
Unzipping /Applications/DevEco-Studio.app/Contents/tools/ohpm.zip
Initializing ohpm
added 106 packages in 3s
9 packages are looking for funding
run `npm fund` for details
execute install task finished, component ohpm.zip.
 
2.SDK Setup
Install task started: ArkTS 3.2.12.5
Downloading https://contentcenter-drcn.dbankcdn.cn/pub_1/DevEcoSpace_1_900_9/b7/v3/fMjcKBCJRHKV3-4Mm5H6bQ/P0ryC2BASauqeQgRtik8Zw.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/ets/3.2.12.5/install/P0ryC2BASauqeQgRtik8Zw.zip...
Installing ArkTS dependencies...
Running 'npm install'...
> compilier@0.0.1 postinstall
> node npm-install.js
31m 
added 569 packages in 30s
38 packages are looking for funding
  run `npm fund` for details
39m
31m 
added 566 packages in 30s
36 packages are looking for funding
  run `npm fund` for details
39m
added 570 packages in 1m
66 packages are looking for funding
  run `npm fund` for details
'npm install' executed
Moving the SDK...
Install task finished: ArkTS 3.2.12.5
Install task started: Previewer 3.2.12.5
Downloading https://contentcenter-drcn.dbankcdn.cn/pub_1/DevEcoSpace_1_900_9/7b/v3/jXnekaGkSUGTjDDGgfHVnQ/-7QEFk9HSG2WzvbcsxmYEQ.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/previewer/3.2.12.5/install/-7QEFk9HSG2WzvbcsxmYEQ.zip...
Moving the SDK...
Install task finished: Previewer 3.2.12.5
Install task started: JS 3.2.12.5
Downloading https://contentcenter-drcn.dbankcdn.com/pub_1/DevEcoSpace_1_900_9/12/v3/G-bsk1wKTWWP1M-kowQUHg/oAB_lVh9Q8-PM9tLqAzb-Q.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/js/3.2.12.5/install/oAB_lVh9Q8-PM9tLqAzb-Q.zip...
Installing JS dependencies...
Running 'npm install'...
> ace-loader@1.0.11 postinstall
> node npm-install.js
31m 
added 569 packages in 19s
38 packages are looking for funding
  run `npm fund` for details
39m
31m 
added 566 packages in 19s
36 packages are looking for funding
  run `npm fund` for details
39m
added 650 packages in 37s
87 packages are looking for funding
  run `npm fund` for details
'npm install' executed
Moving the SDK...
Install task finished: JS 3.2.12.5
Install task started: Toolchains 3.2.12.5
Downloading https://contentcenter-drcn.dbankcdn.cn/pub_1/DevEcoSpace_1_900_9/6f/v3/MFHQI6UMQpGuZcNjWyXpkg/pBla6R0BRHiob3fULBVngA.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/toolchains/3.2.12.5/install/pBla6R0BRHiob3fULBVngA.zip...
Moving the SDK...
Install task finished: Toolchains 3.2.12.5
Install task started: Previewer 3.2.3.6
Downloading https://update.dbankcdn.com/download/data/pub_13/HWHOTA_hota_900_9/cd/v3/6-Eg0KmCSpOpkqSEm-c8_w/previewer-darwin-arm64-3.2.3.6-Release.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/previewer/3.2.3.6/install/previewer-darwin-arm64-3.2.3.6-Release.zip...
Moving the SDK...
Install task finished: Previewer 3.2.3.6
Install task started: Toolchains 3.2.3.6
Downloading https://update.dbankcdn.com/download/data/pub_13/HWHOTA_hota_900_9/cd/v3/6-Eg0KmCSpOpkqSEm-c8_w/toolchains-darwin-arm64-3.2.3.6-Release.zip...
Unzipping /Users/yiminkuang/Library/Huawei/Sdk/.temp/toolchains/3.2.3.6/install/toolchains-darwin-arm64-3.2.3.6-Release.zip...
Disconnecting from HDC
Moving the SDK...
Install task finished: Toolchains 3.2.3.6
 
Configuration result:
Basic setup successful
SDK setup successful
```