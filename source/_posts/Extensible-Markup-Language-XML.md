---
title: Extensible-Markup-Language-XML
date: 2016-03-03 13:57:50
tags:
    - 很久以前系列
    - HTML
---

#### doctype
之前了解的都不细致，cookbook里面讲的很清楚，document type definition，文档类型声明

为什么它要在第一行呢，因为是它告诉浏览器如何处理文档的，若非，则浏览器进入quirks mode,怪异模式，这样子代码就有可能无法正常运行了吼

```
<!DOCTYPE html>
```

奏是这么清爽，告诉浏览器处于标准模式下

其实很早的时候也是超级简单的。

#### 字符编码

head标记中第一行要包含字符集（charset）的声明,告诉浏览器应该如何解释这个文件。

```
<meta charset="utf-8"/>
```

#### HTML5(降低标记markup，简化调用->不用加type了)

- 语法编写风格->最好闭合所有标记，使用小写字母，用引号括属性
- HTML5没有官方的验证服务。。。
- validator.w3.org
- html5.validator.nu


#### H5

1. 兼容性
2. 文档结构
3. Web APP Function

#### 语法上的改进：

- 内容类型
- doctype声明
- 指定字符编码
- 可以省略标记的元素
- 具有布尔值的属性
- 省略引号

#### 增加:

结构上

其他（video audio canvas）

input

#### 废除：

不再使用frame框架

#### 增加:

- 属性（表单，链接）
- 全局属性：
contentEditable（boolean）

designMode

hidden（boolean）

spellcheck

tabindex(-1)

- 增加的主体结构元素

article（独立性）——>可嵌套，插件，内嵌页面，促进语义化

section（分段，分块）——>1.不要将其作为设置样式的页面容器。2.若article，aside，nav更合适，就放手让它们做吧。3.没有标题内容，不用section

nav:传统导航条，侧边栏，页内，翻页操作

aside：article（内OR外）

time元素

微格式

pubdate属性

- 增加的非主体结构元素

header 可以出现多次

footer 作为其上层父级内容区块或是一个根区块的脚注

hgroup 对多个相关联的H1，H6标题进行分组

address 在文档中呈现联系信息

point.1 显示（隐式）编排内容区域块

- 标题分级

- 不同区域块使用相同标题

- 表单新增元素与属性

form

formaction

formmethod

formenctype

formtarget(在何处打开)

autofocus

required

labels

- 标签的control属性

- 文本框的placeholder属性

- 文本框的list属性

- 文本框的autocomplete属性

- pattern属性（正则验证）

- 文本框的selectionDirection属性->获取用户操作

- 复选框的indeterminate属性

- image提交按钮的height与width属性

### 聊一聊html中有趣的属性

#### map area
MDN指路：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/map

HTML <map> 属性 与 <area> 属性一起使用来定义一个图像映射(一个可点击的链接区域).

name属性 给map一个名字用来查询，这个属性是必须的，值必须不能为空并且不能带空格。name属性不准与同文档中其他map元素的值相同，如果id属性也被添加，name属性和id属性的值必须相同。


<map name="example-map-1">
  <area shape="circle" coords="200,250,25" href="another.htm" />
  <area shape="default" />
</map>



#### Deprecated Tags / Deprecated Attributes
