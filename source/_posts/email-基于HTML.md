---
title: email-基于HTML
date: 2021-09-22 16:00:26
tags:
---
- 参考资料：https://github.com/rodriguezcommaj/frontendmasters

### 限制
- 基础的HTML+CSS
- 基于table的布局
- 简单的语义

### 注意
- CSS 样式重置（MS Office｜ 浏览器客户端 ｜ 超链接）
- HTML标签的选择
  - div|span  && h1-h6 && p|strong|em && img 
- 样式 embedded｜inline style
- CSS选择
  - text: color|font-family|font-size|font-style|font-weight|line-height|text-align
  - block element: margin|padding|width|max-width
- 图片
  - 响应式
  - 文本说明
  - 格式限制：jpg,png,gif
  - max-width:100%;min-width:X;width:100%; 宽度适应
- accessibility
  - 视弱｜色盲
  - 高对比度｜视觉上面的层级｜可读性｜布局简单可用
  - 少使用图片，用真的文字，这样可以通过辅助工具（NVDA，VoiceOver｜JAWS）读出来
  - role="presentation" - table
  - 语义化标签｜图片有文本的alt|标注语言
- table
```
<table border="0" cellpadding="0" cellspacing="0"
role="presentation" width="100%">
<tr>
<td style="styles go here">
</td>
</tr>
</table>
```
- 移动端可读
  - 判断版本
  - 媒体探测

- 交互
  - :hover
  - transition|@keyframes

- 测试
  - 可以用litmus进行测试
  - caniemail.com
  - Campaignmonitor.com/css
  - Freshinbox.com/resources 
  - mjml.io

- 参考
  - TheBetter.Email/resources