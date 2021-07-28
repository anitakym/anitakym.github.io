---
title: flutter开发环境配置
date: 2021-06-24 10:31:09
tags:
---

### 环境配置
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

2. IOS设备开发调试
- 普通调试，Xcode登录开发者帐号，进入项目，双击 xxx/ios/Runner.xcworkspace , 在Runner.xcodeproj Tab下，Targets/Runner , Signing & Capabilities , 里面的 Signing ： 1.勾选Automatically manage signing 2.Team选择登录的帐号的Team； 这样会自动给生成一个临时的签名； 设备插入电脑，就可以识别并安装了；
- 记得关掉iPhone的同步功能，不然会显示设备busy
- 查UDID
设备连接到Mac电脑上
点击设备，显示的信息最上方，可以点击内容切换信息；切到有UDID的，然后右键，选择拷贝UDID即可
- ```flutter run --release ```,可以在ios设备上安装release包，这样不在连接情况下，也能使用

3. andriod设备开发调试
#### 真机调试
- 连上android设备
- 如果flutter doctor出现android方面的问题，可以打开android studio，点击preferences
- 以SDK为关键词搜索，进入到Android SDK 设置的面板，这个时候就可以安装没有安装的SDK
- 下面的问题，Android SDK 面板 - SDK platform里面选择对应版本安装
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
- 如果出现了这个问题，则可以在Android SDK 面板设置 "command line tools",勾选，然后安装
```
flutter doctor --android-licenses
Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/annotation/XmlSchema
	at com.android.repository.api.SchemaModule$SchemaModuleVersion.<init>(SchemaModule.java:156)
```

### 命令查询
```flutter --help```
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