---
title: material-ui
date: 2021-08-17 11:29:45
tags:
---

> 团队要基于 flutter 做 Android 端的产品，研究了下 material-ui；

### history

- Andy Rubin - Android
- ROM 系统（MIUI ｜ FLyme | Smartisan | 联想乐 OS ｜ 华为 ROM）
- 尺寸问题 - PS-cutterman sketch|XD->按尺寸调整
- Material Design 规范（类似 APPLE HIG）
- 2014-googleI/O(https://www.youtube.com/watch?v=97SWYiRtF0Y)

### 文档指南

vscode 可以配置好对应语言使用的拓展，这样可以书包放上去就能看到提示；
https://material.io/design/color/the-color-system.html#color-usage-and-palettes

https://material-io.cn/resources/get-started#design

#### 从设计角度来看的一篇介绍文章

https://www.uisdc.com/material-design-knowledge

#### Web

https://github.com/muicss/mui
https://github.com/Dogfalo/materialize
https://getmdl.io/
https://en.wikipedia.org/wiki/Comparison_of_Material_Design_implementations

#### React:

https://material-ui.com/zh/

#### Flutter

- https://flutter.cn/docs/development/ui/widgets/material
- Flutter 提供了遵循 Material Design 规范的 ThemeData
- https://api.flutter.dev/flutter/material/ThemeData/ThemeData.html (themedata 相关文档)

```

// 全局 ——————
MaterialApp(
  title: 'Flutter Demo',
  theme: ThemeData(
      brightness: Brightness.dark, //明暗
      accentColor: Colors.black, //Widget前景色
      primaryColor: Colors.blue, //主色调
      iconTheme:IconThemeData(color: Colors.cyan),// icon主题色
      textTheme: TextTheme(body1: TextStyle(color: Colors.white)) // 文本颜色
  ),
  home: MyHomePage(title: 'Flutter Demo Home Page'),
);
// 局部覆盖 ——————

// 新建
Theme(
    data: ThemeData(iconTheme: IconThemeData(color: Colors.blue)),
    child: Icon(Icons.favorite)
);

// 继承
Theme(
    data: Theme.of(context).copyWith(iconTheme: IconThemeData(color: Colors.blue)),
    child: Icon(Icons.feedback)
);

// 复用
Theme.of(context)

// 区分平台
初始化时候在theme里面做个判断，分别复制不同主题的配置（defaultTargetPlatform）

```

### 相关阅读推荐

#### 设计相关

- https://blog.nicolesaidy.com/7-steps-to-become-a-ui-ux-designer-8beed7639a95
- https://en.wikipedia.org/wiki/Twelve_basic_principles_of_animation
- https://design.facebook.com/
- https://www.ibm.com/design/language/
- https://bradfrost.com/blog/post/atomic-web-design/
- https://uxplanet.org/the-psychology-principles-every-ui-ux-designer-needs-to-know-24116fd65778
- https://medium.com/thinking-design/the-evolution-of-ui-ux-designers-into-product-designers-623e4e7eaab3

#### 书本推荐

- 简约至上
- dont't make me think

#### 好用的工具

- http://palette.site/ （Chrome 插件，可以抓取网站颜色，生成 palettes）

#### 产品案例

- Primer - 卡片
- Fabulous
