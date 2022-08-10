---
title: flutter-webview
date: 2021-08-09 14:12:43
tags:
---

### debugging

https://inappwebview.dev/docs/debugging-webviews/

### packages

https://pub.dev/packages/webview_flutter

#### Android

- on Android the WebView widget is backed by a WebView.
- https://developer.android.com/reference/android/webkit/WebView
- https://flutter.dev/docs/development/platform-integration/platform-views

#### IOS

- https://developer.apple.com/documentation/webkit/wkwebview

### Tips
#### HTTP
- iOS默认会白屏
- android9.0以上版本也会限制访问
- info.list | AndroidManifest.xml

#### mode
- When building your application in release mode, Flutter apps can be compiled for armeabi-v7a (ARM 32-bit), arm64-v8a (ARM 64-bit), and x86-64 (x86 64-bit). Flutter does not currently support building for x86 Android.
- https://flutter.dev/docs/deployment/android#what-are-the-supported-target-architectures



### h5对接第三方，webview版本低会导致的问题
#### cases
- padStart 支持
- 


### WKWebView 请求拦截探索与实践

- https://juejin.cn/post/6922625242796032007