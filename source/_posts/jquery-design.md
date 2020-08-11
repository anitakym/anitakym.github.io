---
title: jquery-design
date: 2020-08-11 11:31:11
tags:
    - jquery
---
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
