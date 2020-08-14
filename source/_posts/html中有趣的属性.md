---
title: html中有趣的属性
date: 2018-11-28 14:49:18
tags:
  - html
---
> 聊一聊html中有趣的属性

#### map area
MDN指路：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/map

HTML <map> 属性 与 <area> 属性一起使用来定义一个图像映射(一个可点击的链接区域).

name属性 给map一个名字用来查询，这个属性是必须的，值必须不能为空并且不能带空格。name属性不准与同文档中其他map元素的值相同，如果id属性也被添加，name属性和id属性的值必须相同。


<map name="example-map-1">
  <area shape="circle" coords="200,250,25" href="another.htm" />
  <area shape="default" />
</map>



#### Deprecated Tags / Deprecated Attributes
