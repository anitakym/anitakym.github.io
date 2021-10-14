---
title: dart-sass
date: 2021-09-18 10:47:50
tags:
---

### 为啥要说这个
vue-cli , create的时候，如果选择手动，在配置CSS预处理器的时候，提供了dart-sass 和 node-sass的选择；
```
Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported 
by default): (Use arrow keys)
❯ Sass/SCSS (with dart-sass) 
  Sass/SCSS (with node-sass) 
  Less 
  Stylus
```

想到了若干年前，之前项目node-sass安装时候，网络的问题

### 存在问题
elementui的icon.scss
里面的
content的unicode会在loader sass-dart 处理过程中被转成  等字符，从而导致浏览器 接收css文件的时候如果编码方式有问题，会变成"î›»"，进而影响渲染；

#### 解决方案
issue讨论：https://github.com/PanJiaChen/vue-element-admin/issues/3526
- "sass": "1.39.0",
- @charset 'UTF-8';(src/styles/element-variables.scss)
- (vue.config.js)
```
css: {
    loaderOptions: {
      sass: {
        sassOptions: { outputStyle: 'expanded' }
      }
    }
  },

```