---
title: 聊聊lodash
date: 2021-03-17 18:11:22
tags:
---

## 实例

### debounce
项目中写的
```
export function debounce(fn, ms) {
  let debounceTimer = null
  return function (...args) {
    if (debounceTimer) clearTimeout(debounceTimer)
    debounceTimer = setTimeout(() => {
      fn.apply(this, args)
    }, ms);
  }
}

```
lodash中
```
https://github.com/lodash
https://github.com/lodash/lodash/blob/master/debounce.js
代码不摘录了
```

### html-webpack-plugin
- https://www.npmjs.com/package/html-webpack-plugin

options - useroptions
Options: You can pass a hash of configuration options to html-webpack-plugin. Allowed values are as follows:

```
{
  entry: 'index.js',
  output: {
    path: __dirname + '/dist',
    filename: 'index_bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'My App', // options
      filename: 'assets/admin.html'  // options
    })
  ]
}

// The following part renders the template with lodash as a minimalistic loader
const template = _.template(source, { interpolate: /<%=([\s\S]+?)%>/g, variable: 'data', ...options });
```
里面变量替换加渲染，默认的是基于loadash的template使用的
https://lodash.com/docs/4.17.15#template
