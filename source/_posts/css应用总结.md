---
title: css应用总结
date: 2021-10-09 18:35:06
tags:
---
### 分页
> 做的PDF打印的服务

#### break
- 用于模版的分页处理
- block元素（不脱离文档流，非弹性布局）
- page-break-after | page-break-before | page-break-inside
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/page-break-after
- break-after
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/break-after
- inside用avoid，避免元素被分割，例如本项目中题目index|tag|icon等元素(page-break-inside: avoid;)
- after用always，在需要插入分页的地方使用

#### orphans | windows

### css
```
reset.css # 所有样式都被消除
normalize.css # 更合适
# 引入第三方样式库之后，可以看看他们对全局样式的处理，再决定自己要不要做
```
#### box-sizing
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing
- 
```
Note: 对于新的web站点，你可能希望首先将box-sizing设置为border-box，如下所示：

* { box-sizing: border-box; }

这使得处理元素大小的工作变得容易得多，并且通常消除了在布局内容时可能遇到的许多陷阱。然而，在某些情况下，你应谨慎使用这个属性。例如： 你正在编写一个将由其他人使用的共享组件库，如果他们网站的其余部分没有设置此值，他们可能会发现很难使用你的组件库。
```

#### outline
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline
```
border 和 outline 很类似，但有如下区别：

outline不占据空间，绘制于元素内容周围。
根据规范，outline通常是矩形，但也可以是非矩形的

```

#### :focus | :hover

#### mask处理
可以写个mask
<div class="xxx-xxx-mask"></div>
<div class="xxx-xxx"></div>
可以用结构的方法调


#### calc()
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/calc()
- 应用在嵌入到IOS，Android的应用的服务项前端页面


#### white-space
- 富文本相关的录入和渲染，英语学科对 
`white-space: pre-wrap; work-break:work-break; text-align:justify;`
- 这个会在Safari`text-align:justify;` 不生效； Safari 只设置 `text-align:justify;`才能生效；
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/white-space


#### hover 
- https://developer.mozilla.org/en-US/docs/Web/CSS/@media/any-hover
- 媒体查询，可以判断hover的可用性
- https://caniuse.com/?search=hover
- can i use - See full reference on MDN Web Docs. As of Safari for iOS 7.1.2, tapping a clickable element causes the element to enter the :hover state. The element will remain in the :hover state until a different element has entered the :hover state.
- js - window.matchMedia('(any-hover: hover)');


## unocss
- https://antfu.me/posts/reimagine-atomic-css-zh 
- 基本上上面这篇看完了就知道了
- 原子化CSS
```
John Polacek 在 文章 Let’s Define Exactly What Atomic CSS is 中写道：
Atomic CSS is the approach to CSS architecture that favors small, single-purpose classes with names based on visual function.
译文：
原子化 CSS 是一种 CSS 的架构方式，它倾向于小巧且用途单一的 class，并且会以视觉效果进行命名。
```

#### querySelector | querySelectorAll
- 如果选择器是一个ID，并且这个ID错误使用多次，返回第一个匹配该ID的元素
- CSS伪类不会返回任何元素，selectors API

#### object-fit/object-position
- css3
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/object-fit


#### em | rem
- em相对于父元素，rem相对于根元素
- r - root

- 子元素字体大小的em是相对于父元素字体大小
- 元素的width/height/padding/margin用em的话是相对于该元素的font-size
- rem是全部的长度都相对于根元素(一般为<html>)

#### BFC 
```
Block Formatting Context
- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context
- 页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素, 反之也如此
- 因为BFC内部的元素和外部的元素绝对不会互相影响，因此， 当BFC外部存在浮动时，它不应该影响BFC内部Box的布局，BFC会通过变窄，而不与浮动有重叠。同样的，当BFC内部有浮动时，为了不影响外部元素的布局，BFC计算高度时会包括浮动的高度。避免margin 重叠也是这样的一个道理。
clear:both BFC/haslayout
zoom:1(IE6/IE7)
.clearfix:after { content:"; display:block; height:0; overflow:hidden; clear:both; }
.clearfix{ *zoom:!; }
.clearfix 应用在包含浮动子元素的父级元素上
```

#### 定位
```
内凹圆角
学会组合，拆解图形
linear-gradient()
径向渐变
relative/absolute
限制定位 ab:  left:0 top:0
限制层级
限制超越overflow
overflow：hidden 不能限制ab 但是加了relative，可以了
relative、fixed 限制z-index层级
relative，定位特性 相对自身定位 无侵入定位：自定义拖拽
top/bottom left/right 绝对定位是拉伸 相对定位是斗争（top,left）
relative 提高层叠上下文
dom流后面覆盖前面
position：relative(提高层级)
relative z-index :auto->不限制内部absolute层叠问题
IE6，7下，容易出现层级覆盖bug
relative的最小化影响原则
```

### ifc / bfc / 盒模型
- 格式化上下文 - 决定渲染区域内节点的排版，关系和互相作用的渲染规则
- https://zhuanlan.zhihu.com/p/110617108

### @charset @import
- https://developer.mozilla.org/en-US/docs/Web/CSS/@import
- https://developer.mozilla.org/en-US/docs/Web/CSS/@charset
```
Imported rules must come before all other types of rules, except @charset rules and layer creating @layer statements. The @import rule is not a nested statement. Therefore, it cannot be used inside conditional group at-rules.
```

### CSS模块化
class名 + hash值


### CSS Hack
- IE8以下
```
<!--[if IE]>
	<style>
	.zzz {
	}
	</style>
	<![endif]-->
```
- Avoid CSS Expressions

#### 微观现象
- 换行编写行内元素，排版会出现5px空隙
- 行内元素统一以底边垂直对齐
- 排版若一行无法完成则换行接着排版

#### 文档流
- 节点参与浮动布局后，自身脱流但其文本不脱流
- 节点参与定位布局后，自身及其文本一起脱流

#### z-index
- 层叠上下文指盒模型在三维空间Z轴中的表现行为
- z-index只在声明定位的节点中起效
- 节点在Z轴的层叠顺序根据z-index、层叠上下文和层叠等级共同决定
