---
title: ios-Frameworks-summary
date: 2023-04-18 16:34:50
tags:
---
- framework是一个有层级的目录
- 讲动态代码库，nib  files, 图片文件，头文件和参考文件全部封装成一个单一的资源包
- 对于Xcode, framework是一个文件后缀为.framework的文件包

### ios 系统框架
UIKit：UIKit是iOS开发中最重要的框架之一，它为应用程序提供了各种用户界面元素和控件，如标签、按钮和文本字段等。

Foundation：Foundation框架提供了许多基本的数据类型和工具，如字符串、日期和网络通信等，用于处理iOS应用程序的核心功能。

Core Data：Core Data是一个对象关系映射框架，用于管理应用程序的数据模型，并提供对持久化储存的支持。

Core Animation：Core Animation是一个强大的动画框架，可用于创建流畅的界面过渡和动画效果。

Core Location：Core Location提供了访问iOS设备位置信息的API，可以用于创建地图、导航和其他位置相关应用程序。

Metal：Metal框架是一个高性能的图形渲染框架，用于创建游戏和其他图形密集型应用程序。

AVFoundation：AVFoundation框架提供了音频和视频处理的API，可用于创建多媒体应用程序和游戏。

### 系统框架分层
iOS系统框架可以分为四个层次，从最底层到最顶层依次是：

#### Core OS层：
Core OS层提供了操作系统的核心功能，包括内存管理、文件系统、安全和网络等。

#### Core Services层：
Core Services层构建在Core OS层之上，提供了更高级别的系统服务，如网络通信、数据管理、XML解析和位置服务等。

#### Media层：
Media层提供了音频、视频和图形处理功能，包括相机、媒体播放器和基于OpenGL ES的图形渲染引擎等。

#### Cocoa Touch层：
Cocoa Touch层是iOS应用程序开发的核心，提供了用户界面元素、多点触摸手势、加速计和硬件访问等API，以及其他框架如Core Data和Core Animation等。