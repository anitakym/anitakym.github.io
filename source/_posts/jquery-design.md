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

#### 拓展
我们可以扩展jquery来实现自定义方法—— 编写jquery插件
```

```

