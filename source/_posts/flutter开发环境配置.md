---
title: flutter开发环境配置
date: 2021-06-24 10:31:09
tags:
---


问题:
1. 执行flutter doctor之后，出现这个
```
[!] Xcode - develop for iOS and macOS
    ✗ CocoaPods installed but not working.
        You appear to have CocoaPods installed but it is not working.
        This can happen if the version of Ruby that CocoaPods was installed with is different from the one being used to invoke it.
        This can usually be fixed by re-installing CocoaPods.
      To re-install see https://guides.cocoapods.org/using/getting-started.html#installation for instructions.
```
```
brew cleanup -d -v
brew install cocoapods | brew upgrade cocoapods
```
如果提示failed to link, brew link cocoapods

2. 查UDID
设备连接到Mac电脑上
点击设备，显示的信息最上方，可以点击内容切换信息；切到有UDID的，然后右键，选择拷贝UDID即可