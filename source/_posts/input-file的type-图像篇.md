---
title: input-file的type-图像篇
date: 2020-06-06 16:55:51
tags:
    - 基础篇
---
![](inputfile.png)
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file

## basic
### File API
- https://w3c.github.io/FileAPI/
- https://juejin.cn/post/6857065289532735502
### 超好用的Blob对象
https://github.com/akira-cn/FE_You_dont_know/issues/12



## 其他
- https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input
- input的type为search
- 用于搜索字符串的单行文字区域。输入文本中的换行会被自动去除。在支持的浏览器中可能有一个删除按钮，用于清除整个区域。拥有动态键盘的设备上的回车图标会变成搜索图标
- 如果想去除X，可以通过样式设置
```
input::-webkit-search-cancel-button,
input::-ms-clear {
  display: none;
}
input[type=search] {
    -webkit-appearance: none;
}
```
- form 
```
action
处理表单提交的 URL。这个值可被 <button>、<input type="submit"> 或 <input type="image"> 元素上的 formaction 属性覆盖。
```