---
title: flutter开发环境配置
date: 2021-06-24 10:31:09
tags:
---

### 环境配置

问题:

1. 执行 flutter doctor 之后，出现这个

```
[!] Xcode - develop for iOS and macOS
    ✗ CocoaPods installed but not working.
        You appear to have CocoaPods installed but it is not working.
        This can happen if the version of Ruby that CocoaPods was installed with is different from the one being used to invoke it.
        This can usually be fixed by re-installing CocoaPods.
      To re-install see https://guides.cocoapods.org/using/getting-started.html#installation for instructions.
```

```
# 清理旧版本,Remove stale lock files and outdated downloads for all formulae and casks, and remove old versions of installed formulae. 
brew cleanup -d -v
brew install cocoapods | brew upgrade cocoapods
```

如果提示 failed to link, brew link cocoapods

2. IOS 设备开发调试

- 普通调试，Xcode 登录开发者帐号，进入项目，双击 xxx/ios/Runner.xcworkspace , 在 Runner.xcodeproj Tab 下，Targets/Runner , Signing & Capabilities , 里面的 Signing ： 1.勾选 Automatically manage signing 2.Team 选择登录的帐号的 Team； 这样会自动给生成一个临时的签名； 设备插入电脑，就可以识别并安装了；
- 记得关掉 iPhone 的同步功能，不然会显示设备 busy
- 查 UDID
  设备连接到 Mac 电脑上
  点击设备，显示的信息最上方，可以点击内容切换信息；切到有 UDID 的，然后右键，选择拷贝 UDID 即可
- `flutter run --release `,可以在 ios 设备上安装 release 包，这样不在连接情况下，也能使用

3. android 设备开发调试

#### Android

- 连上 android 设备
- 如果 flutter doctor 出现 android 方面的问题，可以打开 android studio，点击 preferences
- 以 SDK 为关键词搜索，进入到 Android SDK 设置的面板，这个时候就可以安装没有安装的 SDK
- 下面的问题，Android SDK 面板 - SDK platform 里面选择对应版本安装

```
[!] Android toolchain - develop for Android devices (Android SDK version 30.0.3)
    ✗ Android SDK file not found:
      /Users/kuangyimin/Library/Android/sdk/platforms/android-30/android.jar.
```

- 下面的问题，按提示，Run `flutter doctor --android-licenses`

```
[!] Android toolchain - develop for Android devices (Android SDK version 30.0.3)
    ✗ Android license status unknown.
      Run `flutter doctor --android-licenses` to accept the SDK licenses.
      See https://flutter.dev/docs/get-started/install/macos#android-setup for
      more details.
```

- 如果出现了这个问题，则可以在 Android SDK 面板设置 "command line tools",勾选，然后安装

```
flutter doctor --android-licenses
Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/annotation/XmlSchema
	at com.android.repository.api.SchemaModule$SchemaModuleVersion.<init>(SchemaModule.java:156)
```

- 如果 flutter run 的时候提示这个问题，则可以按提示，去 Android Studio，搜 SDK，下载对应缺少的 SDK

```
Could not determine the dependencies of task ':launch_review:compileDebugAidl'.
> Failed to install the following SDK components:
      platforms;android-28 Android SDK Platform 28
  Install the missing components using the SDK manager in Android Studio.
```

- 阿里云镜像配置

```
// 对照表
// https://developer.aliyun.com/mvn/guide
//
buildscript {
    repositories {
        // google()
        // jcenter()
        maven {
            url 'https://maven.aliyun.com/repository/google'
        }
        maven {
            url 'https://maven.aliyun.com/repository/jcenter'
        }
        maven {
            url 'https://maven.aliyun.com/nexus/content/groups/public'
        }
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.4'
    }
}

```
- 开模拟器的时候，如果报"The emulator process for AVD was killed"
原因：没有足够的空间，可以关掉别的占内存的软件；删除虚拟机，重新安装，启动；
show on Disk(可以看到安装的位置)
### 命令查询

`flutter --help`

```
Available commands:
  analyze           Analyze the project's Dart code.
  assemble          Assemble and build Flutter resources.
  attach            Attach to a running app.
  bash-completion   Output command line shell completion setup scripts.
  build             Build an executable app or install bundle.
  channel           List or switch Flutter channels.
  clean             Delete the build/ and .dart_tool/ directories.
  config            Configure Flutter settings.
  create            Create a new Flutter project.
  devices           List all connected devices.
  doctor            Show information about the installed tooling.
  downgrade         Downgrade Flutter to the last active version for the current channel.
  drive             Run integration tests for the project on an attached device or emulator.
  emulators         List, launch and create emulators.
  format            Format one or more Dart files.
  gen-l10n          Generate localizations for the current project.
  install           Install a Flutter app on an attached device.
  logs              Show log output for running Flutter apps.
  precache          Populate the Flutter tool's cache of binary artifacts.
  pub               Commands for managing Flutter packages.
  run               Run your Flutter app on an attached device.
  screenshot        Take a screenshot from a connected device.
  symbolize         Symbolize a stack trace from an AOT-compiled Flutter app.
  test              Run Flutter unit tests for the current project.
  upgrade           Upgrade your copy of Flutter.

Run "flutter help <command>" for more information about a command.
Run "flutter help -v" for verbose help output, including less commonly used options.
```

```
Create a new Flutter project.
If run on a project that already exists, this will repair the project, recreating any files that are missing.
如果想要生成对应iOS，android文件，可以 flutter create .
```

#### 调试问题

```
vm-service: Error: Unhandled exception:
WebSocketException: Invalid WebSocket upgrade request
[VERBOSE-2:dart_isolate.cc(1137)] Unhandled exception:
WebSocketException: Invalid WebSocket upgrade request
Error connecting to the service protocol: failed to connect to http://127.0.0.1:55440/xxxxx=/
```

1. Error connecting to the service protocol: failed to connect to http://127.0.0.1:58661/xxxxx=/
   
2. 问题原因，电脑开了系统代理 | 设备和电脑不在一个网络；
3. 解决方案，关掉系统代理，如果在当前 terminal 里面加了 export 语句，记得关掉，重新打开一个新的终端；如果是外接设备，可以把设备和电脑连接到同一个网络；

#### IOS

1. Specifies the platform for which a static library should be built.

```
podfile:
# Uncomment this line to define a global platform for your project
platform :ios, '9.0'
https://guides.cocoapods.org/syntax/podfile.html#platform
```

2. https://guides.cocoapods.org/syntax/podfile.html
   podfile 的配置
