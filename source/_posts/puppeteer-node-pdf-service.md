---
title: puppeteer-node-pdf-service
date: 2021-03-19 16:30:34
tags:
---
不涉及业务，讲一下技术方面PDF生成服务的心得

### 文档指北：
- puppeteer(https://github.com/puppeteer/puppeteer)
<pre>
Puppeteer is a Node library which provides a high-level API to control Chrome or Chromium over the DevTools Protocol. Puppeteer runs headless by default, but can be configured to run full (non-headless) Chrome or Chromium.
</pre>

应用场景：
1. 页面截图服务
2. PDF生成服务
3. 自动化测试
4. 服务端渲染内容抓取

try:https://try-puppeteer.appspot.com/

就几乎碰到的问题，文档上面都能找到，所以文档和生态还是比较完备的
https://github.com/puppeteer/puppeteer/blob/main/docs/api.md


也有troubleShooting的文档：
https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md

## History

### 几次技术改造

- downloadCenter
- 从接口获取模版渲染数据 -> 从mongodb获取
- XX_report 进度状态原先由接口返回 -> 返回到mq
- node服务本身 - 配合修改+日志+调试配置开关


### 部署和CI优化
#### 底层脚本
- pm2配置
```
```

#### Jenkins可视化集成


## 项目代码分析

### module本身使用代码风格不是很清晰明确
- https://github.com/chemdemo/chemdemo.github.io/issues/2
- exports.xxx | module.exports = xxx

### process
- beforeExit
- 

## 字体相关

### 页眉页脚中文字体
- https://www.npmjs.com/package/pdf-lib#embed-font-and-measure-text
- https://github.com/Hopding/pdf-lib/issues/430
- 额外引入一些特殊的中文字体，如果直接用pdf-lib，@pdf-lib/fontkit（旧版本） ，则需配合font-carrier进行字体精简
- https://www.npmjs.com/package/pdfkit， pdfkit则不用，默认精简
- @pdf-lib/fontkit - https://github.com/Hopding/fontkit , https://github.com/foliojs/fontkit
```
# https://www.npmjs.com/package/font-carrier
案例三
对中文字体精简

var fontCarrier = require('font-carrier')
var transFont = fontCarrier.transfer('./test/test.ttf')
// 会自动根据当前的输入的文字过滤精简字体
transFont.min('我是精简后的字体，我可以重复')
transFont.output({
  path: './min'
})
```
```
const fontkit = require('@pdf-lib/fontkit');
doc.registerFontkit(fontkit); // 注册字体
# 如果直接用的话，则默认无裁剪，会导致生成的PDF文件过大
# 可以利用font-carrier解决
const fontCarrier = require('font-carrier');
const transFont = fontCarrier.transfer(`${dir}/font/pingfang.ttf`);
transFont.min(headerFooter.title.join('') + extra + '.');
const fontMinResult = transFont.output({
    types:['ttf']
  });
  // 加载自定义字体
const customFont = doc.embedFont(fontMinResult.ttf);
```
```
# 较新版本支持subset
const subset = font.createSubset();
run.glyphs.forEach(function(glyph) {
  subset.includeGlyph(glyph);
});

subset.encodeStream()
      .pipe(fs.createWriteStream('subset.ttf'));
```

### 割字问题
保证内容里面不想被切割的，为块装结构

### echarts部分图丢失
升级puppteer

### ttf2woff2 (dep by font-carrier)
- https://www.npmjs.com/package/ttf2woff2
- This is a NodeJS wrapper for the Google WOFF2 project. If the C++ wrapper compilation fail, it fallbacks to an Emscripten build.
- Convert TTF files to WOFF2 ones.

