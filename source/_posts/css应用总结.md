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
- inside用avoid，避免元素被分割，例如本项目中题目index|tag|icon等元素
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