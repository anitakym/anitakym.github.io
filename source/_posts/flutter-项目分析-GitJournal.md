---
title: flutter-项目分析-GitJournal
date: 2021-08-20 11:43:48
tags:
---

## 背景

### 项目地址

### packages

#### time 2.0.0

- https://pub.dev/packages/time

## 功能点分析

#### 用户权限申请

- https://pub.dev/packages/permission_handler

```
permission_handler:
    dependency: "direct main"
    description:
      name: permission_handler
      url: "https://pub.dartlang.org"
    source: hosted
    version: "6.1.1"
  permission_handler_platform_interface:
    dependency: transitive
    description:
      name: permission_handler_platform_interface
      url: "https://pub.dartlang.org"
    source: hosted
    version: "3.1.1"
```

```
<!-- android/app/src/main/AndroidManifest.xml -->
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="com.android.vending.BILLING" />
    <uses-feature android:name="android.hardware.camera" android:required="false" />

    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_INTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

#### 引导页
