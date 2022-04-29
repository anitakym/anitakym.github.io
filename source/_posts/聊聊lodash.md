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


### 类型判断
- 里面提供了一些类型判断的方法
- 哈哈哈，但是呢，还有一个项目
- https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore
- 可见下面的is系列-在lodash里面grep is
```
isArguments.js
isArrayBuffer.js
isArrayLike.js
isArrayLikeObject.js
isBoolean.js
isBuffer.js
isDate.js
isElement.js
isEmpty.js
isEqualWith.js
isError.js
isFunction.js
isLength.js
isMap.js
isMatch.js
isMatchWith.js
isNative.js
isNil.js
isNull.js
isNumber.js
isObject.js
isObjectLike.js
isPlainObject.js
isRegExp.js
isSet.js
isString.js
isSymbol.js
isTypedArray.js
isUndefined.js
isWeakMap.js
isWeakSet.js
```
- 同样，可以看看You-Dont-Need-Lodash-Underscore里面给出的原生方法可以给到的实现
