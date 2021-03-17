---
title: 聊聊lodash
date: 2021-03-17 18:11:22
tags:
---
html-webpack-plugin

options

useroptions

```
// The following part renders the template with lodash as a minimalistic loader
  //
  const template = _.template(source, { interpolate: /<%=([\s\S]+?)%>/g, variable: 'data', ...options });
```
里面变量替换加渲染，默认的是基于loadash的template使用的
https://lodash.com/docs/4.17.15#template
