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
#### why
- 不同浏览器不同版本，支持的字体格式不一样；
- 我们可以设计一些图标占字体的坑，从而可以像操作字一样操作图标（矢量的）
- 使用 - 1.font-face声明字体 2.定义使用iconfont的样式 3. <i class="iconfont">&#x0032</i> （unicode） 4.:before :after等伪元素 content:"\0032"; （16进制）
- 注意设备跨域问题的兼容
- -webkit-font-smoothing: antialiased; （解决字体图标存在半个像素的锯齿，在浏览器渲染时为一个像素，从而看起来加粗）
- ie使用16进制unicode的时候加；号

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
