---
title: jquery-design
date: 2020-08-11 11:31:11
tags:
    - jquery
---

> 一般我看源码的tricks，找到core.js,一些精简的库，cmd+J,cmd+K,cmd+0（VSCode）;得到方法折叠，然后再一层层展开看结构；
> jQuery 阶段性的选择，在那个阶段，解决了那个阶段的问题；
> github彻底移除jquery - blog( why | how )

## 设计理念
### 回归增强
- Regressive Enhancement
- 为系统的特性设定基线，并应用到较老的设备和浏览器中
### dir
- 3.1.0
```
➜  jquery tree
.
├── AUTHORS.txt
├── LICENSE.txt
├── README.md
├── brower.json
├── dist
│   ├── core.js
│   ├── jquery.js
│   ├── jquery.min.js
│   ├── jquery.min.map
│   ├── jquery.slim.js
│   ├── jquery.slim.min.js
│   └── jquery.slim.min.map
├── external
│   └── sizzle
│       └── dist
│           └── LICENSE.txt
├── package.json
└── src
    ├── ajax
    │   ├── jsonp.js
    │   ├── load.js
    │   ├── parseXML.js
    │   ├── script.js
    │   ├── var
    │   │   ├── location.js
    │   │   ├── nonce.js
    │   │   └── rquery.js
    │   └── xhr.js
    ├── ajax.js
    ├── attributes
    │   ├── attr.js
    │   ├── classes.js
    │   ├── prop.js
    │   ├── support.js
    │   └── val.js
    ├── attributes.js
    ├── callbacks.js
    ├── core
    │   ├── DOMEval.js
    │   ├── access.js
    │   ├── init.js
    │   ├── parseHTML.js
    │   ├── ready-no-deferred.js
    │   ├── ready.js
    │   ├── readyException.js
    │   ├── support.js
    │   └── var
    │       └── rsingleTag.js
    ├── core.js
    ├── css
    │   ├── addGetHookIf.js
    │   ├── adjustCSS.js
    │   ├── curCss.js
    │   ├── hiddenVisibleSelector.js
    │   ├── showHide.js
    │   ├── support.js
    │   └── var
    │       ├── cssExpand.js
    │       ├── getStyles.js
    │       ├── isHiddenWithinTree.js
    │       ├── rmargin.js
    │       ├── rnumnonpx.js
    │       └── swap.js
    ├── css.js
    ├── data
    │   ├── Data.js
    │   └── var
    │       ├── acceptData.js
    │       ├── dataPriv.js
    │       └── dataUser.js
    ├── data.js
    ├── deferred
    │   └── exceptionHook.js
    ├── deferred.js
    ├── deprecated.js
    ├── dlimensions.js
    ├── effects
    │   ├── Tween.js
    │   └── animatedSelector.js
    ├── effects.js
    ├── event
    │   ├── ajax.js
    │   ├── alias.js
    │   ├── focusin.js
    │   ├── support.js
    │   └── trigger.js
    ├── event.js
    ├── exports
    │   ├── amd.js
    │   └── global.js
    ├── jquery.js
    ├── manipulation
    │   ├── _evalUrl.js
    │   ├── buildFragment.js
    │   ├── getAll.js
    │   ├── setGlobalEval.js
    │   ├── support.js
    │   ├── var
    │   │   ├── rcheckableType.js
    │   │   ├── rscriptType.js
    │   │   └── rtagName.js
    │   └── wrapMap.js
    ├── manipulation.js
    ├── offset.js
    ├── queue
    │   └── delay.js
    ├── queue.js
    ├── selector-native.js
    ├── selector-sizzle.js
    ├── selector.js
    ├── serialize.js
    ├── traversing
    │   └── var
    │       └── findFilter.js
    ├── traversing.js
    ├── var
    │   ├── ObjectFunctionString.js
    │   ├── arr.js
    │   ├── class2type.js
    │   ├── concat.js
    │   ├── document.js
    │   ├── documentElement.js
    │   ├── fnToString.js
    │   ├── getProto.js
    │   ├── hasOwn.js
    │   ├── indexOf.js
    │   ├── pnum.js
    │   ├── push.js
    │   ├── rcssNum.js
    │   ├── rnotwhile.js
    │   ├── slice.js
    │   ├── support.js
    │   └── toString.js
    └── wrap.js

24 directories, 110 files
```
#### $
$ 本质是个函数

```
$
jQuery.noConflict()
$
jQuery
```
jQuery在占用$之前，先保存了原来的$,调用jQuery.noConflict()时会把原来保存的变量还原

#### 选择器
- 层级选择器
- 子选择器
- 过滤器
- 表单相关

#### example
data() 方法向被选元素附加数据，或者从被选元素获取数据。
self.find('#xxx tr:last').data().id = rows.sub_categories[i].id;
self.find("#xxx").children().eq(i).data("id")

#### 扩展
我们可以扩展jquery来实现自定义方法—— 编写jquery插件
```
$.fn.testfunc = function() {
  this.css('color', '#fffceb');
  return this; // 因为jquery对象支持链式操作，扩展方法也要能继续链式下去
}
$.fn.testfunc.defaults = {
  color: '#ffffff'
}
```
默认值处理： || && (可以这么处理)

编写插件原则：
1. 给$.fn绑定函数，实现插件的代码逻辑；
2. 插件函数最后要return this，以支持链式调用；
3. 插件函数要有默认值，绑定在$.fn.<pluginName>.defaults上；
4. 调用时可传入设定值以便覆盖默认值
5. 过滤特定元素


### 一些jquery的项目
- The No Hassle JavaScript Colorpicker（bgrins.github.io/spectrum/）
- 

## basics
### module.js
```
;(function(){
  'use strict'
})();
# 自执行函数
# 第一个;是为了如果代码混淆之后，前面的代码如果没有分号，可以避免问题；
# 为什么要放在这个里面，避免全局污染；如果直接var a = 1; 则 window.a = 1;
```

## Others
React17:
```
before17:
document.addEventListener() 来监听事件
17:
rootNode.addEventListener()

# 解决了多版本 React 的问题
# 在和 JQuery 一起使用时，降低事件冲突的可能性
```