---
title: browser相关-一些总结
date: 2021-09-17 16:47:43
tags:
---

###
- https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/
- loupe
### DTD

### 占有率
- https://gs.statcounter.com/browser-market-share/ 


## 问题处理
### 清除所有cookie相关
同样项目，起本地前端服务调试的时候，一个同事的电脑请求返回如下
```
{"status":0,"message":"com.google.gson.stream.MalformedJsonException: Unterminated string at line 1 column 7 path $.","data":null}

```
清除了浏览器的所有application里面cookies等缓存，再次请求就好了

服务端日志是入参被截断了；

### browserslist
- Share target browsers between different front-end tools, like Autoprefixer, Stylelint and babel-preset-env.
- caniuse
- https://github.com/browserslist/browserslist

### caniuse
```
Browserslist: caniuse-lite is outdated. Please run:
npx browserslist@latest --update-db
Why you should do it regularly: https://github.com/browserslist/browserslist#browsers-data-updating
```

### favicon - favorite icon -website icon - page icon - urlicon
- `<link rel="icon" href="/favicon.ico">`
## 性能
- 10年前的 - yslow - https://github.com/marcelduran/yslow - http://yslow.org/


### 浏览器兼容性真机测试
- https://live.browserstack.com/
- browser stack
- 不方便的点可能是没有一些国产浏览器的选项

## history
- 市场占有 https://gs.statcounter.com/
#### 渲染引擎
 Google Chrome：Webkit(前期 1-28)、Blink(后期 28+)
 Apple Safari：Webkit 1+
 Mozilla Firefox：Gecko 1+
 ASA Opera：Presto(前期 7-14)、Blink(后期 15+)
 Microsoft IExplorer：Trident 4+
 Microsoft Edge：Trident(前期)、Blink(后期)

 #### 国产浏览器 极速模式｜兼容模式
 - 双内核
 - 极速模式 - blink内核
 - 兼容模式 - Trident内核（政务网站，金融网站等）

 #### 浏览器私有属性
 - -webkit- -moz- -ms- -o-
 - 厂商 ｜ W3C组织
 - 兼容性写法前，标准写法最后
 - webpack postcss-loader | postcss-preset-env(autoprefixer-caniuse)

 #### 外观属性 ｜ 几何属性
 - 几何属性（布局｜尺寸）- 可用数学几何衡量的属性
 - 外观属性（界面｜文字）- 可用状态向量描述的属性