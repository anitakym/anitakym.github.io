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


### sourcemap 上传问题
- https://docs.sentry.io/platforms/javascript/guides/vue/sourcemaps/troubleshooting_js/
- sentry-cli 上传的时候
- 先排除本身map的问题，及上传的问题（可以通过本地看map的解析及上传log日志里面的信息，sentry管理端上面的文件确认）
- 确保路径的匹配，按照上面的文档
