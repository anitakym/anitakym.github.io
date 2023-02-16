---
title: IOS-APP相关summary
date: 2023-01-22 22:48:41
tags:
---
## APP
#### 展示界面
- 底部TabBar
- navigation导航
- 列表
- 图片imageview
- button/label
- textview
- webview

#### 动画

#### 通用技术架构
- 网络
- 存储
- 图片
- 音频
- 视频
- 数据解析
- 布局/渲染
- 启动
- 日志系统
- 上报系统

## tools
#### xcode
https://help.apple.com/xcode/mac/current

## pre
#### subModule
- git
- 使用简单｜功能少，只能下载全部项目
- debug方便

#### CocoaPods
- ruby
- 中心化管理，生产workspace
- debug方便

#### Carthage
- swift
- 去中心化的管理，提供framework文件
- debug不便

#### MVC in IOS
- View - UIView
- Controller - UIViewController

#### UIView
- 最基础的视图类
- 管理屏幕上一定区域的内容展示
- 作为各种视图类型的父类，提供基础的能力
- 外观，渲染和动画
- 相应区域内的事件
- 布局（设置大小，位置frame ｜ addSubView）
- 使用栈管理管理全部的子视图（位置重叠的展示最后入栈的｜可以随时调整位置｜插入到指定位置）

#### UIViewController
- 视图控制器，管理View层级结构
- 自身包含View，可以理解为一个容器（管理View的生命周期，响应用户操作，和APP整体交互，视图的切换，作为container管理多个Controller和动画）
- ViewController生命周期
```
init
viewDidLoad
viewWillAppear
viewDidAppear
viewWillDisappear
viewDidDisappear
Dealloc
```
#### 页面结构
- 单页面展示（列表展示简介，较长滚动页面展示内容）
- 多页面管理（4，5个底部按钮，通过push的方式进行页面切换）

#### UITabBarController
- 管理多个UIViewController切换

#### UITabBar
#### TabBar实现
- 使用系统函数实现
- 相关开源项目框架和项目
#### UINavigationController
- 通过栈管理页面间的调整
- 通常只展示栈顶页面
- push/pop操作
- 通过UINavigationBar响应操作，处理UIViewController的切换
#### UINavigationBar
- UINavigationController管理
- 顶部UIViewController变化，UINavigationBar同步变化
#### Navigation实现
- 使用系统函数实现
- 相关开源项目框架和项目（开源Navigation相关集中在过渡动画的样式上）

#### UIWindow
- 特殊形式的UIView，提供App中展示内容的基础窗口
- 只作为容器，和ViewController一起协同工作
- 通常屏幕上只存在、展示一个UIWindow
- storyboard会帮我们自动创建
- 手动创建（UIWindow｜rootViewController｜makeKeyAndVisible）
### 签名




### 证书



### 常用iOS唯一标识符


### 打包




### 上架流程


## 线上问题处理

#### 用户反馈登录验证码无法收到
- 需要调用服务端接口
- 接口无响应或者报错
- 查看bonree埋点(用户会话只保留一周)
- 因为没有登录，所以无法根据用户id查，只能用时间查异常会话了，查网络错误的
- 发现对应会话日志提示（URLSessionTask failed with error:此服务器证书无效）
- 辅助信息，对应设备在使用同样产品的微信小程序端时，也有request：fail errorcode:-201的提示，对应状态码是SSL证书过期或者无效的提示
- 同样的网络情况下，别的请求都正常，只是涉及到我们的域的请求有问题
- 查了下证书日期，快到期了，让用户调整了系统时间，解决，我们这边也及时续期