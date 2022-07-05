---
title: sentry-问题处理-summary
date: 2022-07-05 17:38:38
tags:
---
#### 1
ResizeObserver loop limit exceeded
https://github.com/ElemeFE/element/issues/11420#issuecomment-898992179
el-scrollbar
```
main.js
mounted() {
  if (this.native) return;
  this.$nextTick(this.update);
  !this.noresize && addResizeListener(this.$refs.resize, this.update);
},

export const addResizeListener = function(element, fn) {
  if (isServer) return;
  if (!element.__resizeListeners__) {
    element.__resizeListeners__ = [];
    element.__ro__ = new ResizeObserver(resizeHandler);
    element.__ro__.observe(element);
  }
  element.__resizeListeners__.push(fn);
};
```
#### 2
chrome - 102
EvalError: Possible side-effect in debug-evaluate

https://stackoverflow.com/questions/72396527/evalerror-possible-side-effect-in-debug-evaluate-in-google-chrome

console => 设置 => eager evaluation

https://chromium-review.googlesource.com/c/v8/v8/+/3557234/
https://chromium-review.googlesource.com/c/v8/v8/+/3660253


- SyntaxError ?(<unknown module>)
Unhandled
Unexpected end of input
在EvalError: Possible side-effect in debug-evaluate 之后