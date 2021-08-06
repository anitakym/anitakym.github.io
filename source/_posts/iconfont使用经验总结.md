---
title: iconfont使用经验总结
date: 2021-06-22 15:33:36
tags:
---

### 地址

https://www.iconfont.cn/

Tips:

- 做好权限管理，如果有人员变更，保证项目仓库的维护的及时
- 写好操作指南-团队文档

### 操作指南及原理说明

#### 官方文档

https://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.d8cf4382a&helptype=code

#### tips

切记单色

#### trick

如果想要有渐变色什么的，可以背景色设置，然后字弄成透明的

#### 操作指南

1. 为开发成员增加项目权限

2. 位置

```
项目中引用位置：
src/main.js
=> import '@/assets/font/iconfont.css'
文件存放位置：
src/assets/font
```

3. 修改方式：

```
1. 从iconfont下载代码（Font class=>下载至本地），替换原有src/assets/font文件夹
2. 然后修改iconfont.css文件，在第18行增加下面代码：

[class^="el-icon-third"],
[class*=" el-icon-third"]
{
font-family: "iconfont" !important;
font-size: 16px;
font-style: normal;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
}
```

4. 使用方式：
   直接在根据 class 名称(选择 Font Class,然后点复制代码)引用即可，名称可在 iconfont.css 查看，如果觉得名称有问题，可以在 iconfont 网站上面修改，然后更新 font 文件夹。
   `<i class="el-icon-third-share" />`
