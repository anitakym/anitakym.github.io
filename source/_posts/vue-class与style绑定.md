---
title: vue-class与style绑定
date: 2021-03-23 14:20:43
tags:
---
文档链接：
https://v3.cn.vuejs.org/guide/class-and-style.html#%E7%BB%91%E5%AE%9A-html-class
> 操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是 attribute，所以我们可以用 v-bind 处理它们：只需要通过表达式计算出字符串结果即可。不过，字符串拼接麻烦且易错。因此，在将 v-bind 用于 class 和 style 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。

具体使用见文档

- 绑定HTML Class
  - 对象语法
  - 数组语法
  - 在组件上使用

#### code-review:
:class在使用对象和数组语法的时候，团队中，对象语法使用最多，在数组语法的使用中，部分逻辑是可以简化的，也不需要使用数组语法，具体写作的时候没有做思考。

- 绑定内联样式
  - 对象语法
  - 数组语法
  - 自动添加前缀
  - 多重值
#### code-review:
:style的使用，其实是没有做到样式和结构的分离的，追求语义明确和样式的扩展的话，其实是不推荐使用的；不过看场景，如果能做到语义明确，结构简单，使用的话，也没什么大问题

### 实现原理剖析

```
// https://github.com/vuejs/vue/blob/dev/src/core/vdom/create-element.js
// ref #5318
// necessary to ensure parent re-render when deep bindings like :style and
// :class are used on slot nodes
function registerDeepBindings (data) {
  if (isObject(data.style)) {
    traverse(data.style)
  }
  if (isObject(data.class)) {
    traverse(data.class)
  }
}
```
```
// packages/vue-template-compiler/browser.js
// 文件搜索class
function transformNode (el, options) {
    var warn = options.warn || baseWarn;
    var staticClass = getAndRemoveAttr(el, 'class');
    if (staticClass) {
      var res = parseText(staticClass, options.delimiters);
      if (res) {
        warn(
          "class=\"" + staticClass + "\": " +
          'Interpolation inside attributes has been removed. ' +
          'Use v-bind or the colon shorthand instead. For example, ' +
          'instead of <div class="{{ val }}">, use <div :class="val">.',
          el.rawAttrsMap['class']
        );
      }
    }
    if (staticClass) {
      el.staticClass = JSON.stringify(staticClass);
    }
    var classBinding = getBindingAttr(el, 'class', false /* getStatic */);
    if (classBinding) {
      el.classBinding = classBinding;
    }
  }

  function genData (el) {
    var data = '';
    if (el.staticClass) {
      data += "staticClass:" + (el.staticClass) + ",";
    }
    if (el.classBinding) {
      data += "class:" + (el.classBinding) + ",";
    }
    return data
  }

  var klass = {
    staticKeys: ['staticClass'],
    transformNode: transformNode,
    genData: genData
  };
```

### 相关tips
1.truthy 不是 true，详见 MDN 的解释(https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)。