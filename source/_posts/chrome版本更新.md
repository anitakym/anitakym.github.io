---
title: chrome版本更新
date: 2021-03-15 15:34:37
tags:
    - chrome
---

今天测试老师report了一个在Chrome浏览器上的样式问题，排查了下，88无问题，89有问题 —— 具体查，某个没有用scoped的模块，/deep/没有处理
让具体的开发老师处理了下代码，那为什么渲染会有差异呢，哪部分的处理变更了呢，查了下Chrome的更新文档

在Google直接搜索 web updates
https://developers.google.com/web/updates/2021
https://chromium.googlesource.com/chromium/src/+log/89.0.4389.72..89.0.4389.82?pretty=fuller&n=10000
https://developer.chrome.com/blog/deps-rems-89/

[Deprecation] /deep/ combinator is no longer supported in CSS dynamic profile.It is now effectively no-op, acting as if it were a descendant combinator. /deep/ combinator will be removed, and will be invalid at M65. You should remove it. See https://www.chromestatus.com/features/4964279606312960 for more details.


https://www.chromestatus.com/features#%2Fdeep%2F

https://segmentfault.com/a/1190000021576348

https://www.cnblogs.com/CyLee/p/10006065.html

https://vue-loader.vuejs.org/guide/scoped-css.html#deep-selectors

node_modules/@vue/component-compiler-utils/lib/stylePlugins/scoped.ts
```
node.selector = selectorParser((selectors: any) => {
      selectors.each((selector: any) => {
        let node: any = null

        // find the last child node to insert attribute selector
        selector.each((n: any) => {
          // ">>>" combinator
          // and /deep/ alias for >>>, since >>> doesn't work in SASS
          if (
            n.type === 'combinator' &&
            (n.value === '>>>' || n.value === '/deep/')
          ) {
            n.value = ' '
            n.spaces.before = n.spaces.after = ''
            return false
          }

          // in newer versions of sass, /deep/ support is also dropped, so add a ::v-deep alias
          if (n.type === 'pseudo' && n.value === '::v-deep') {
            n.value = n.spaces.before = n.spaces.after = ''
            return false
          }

          if (n.type !== 'pseudo' && n.type !== 'combinator') {
            node = n
          }
        })

        if (node) {
          node.spaces.after = ''
        } else {
          // For deep selectors & standalone pseudo selectors,
          // the attribute selectors are prepended rather than appended.
          // So all leading spaces must be eliminated to avoid problems.
          selector.first.spaces.before = ''
        }

        selector.insertAfter(
          node,
          selectorParser.attribute({
            attribute: id
          })
        )
      })
    }).processSync(node.selector)
```


从设计角度来说，我们也不推荐使用嵌套过多:
```
Very nested SCSS produces big CSS output and is less reusable than little nested one.

Use nesting to not repeat yourself when scoping of selectors is necessary, not to reflect the document structure.

Supported by: http://youtu.be/fPAf8dN4G4w?t=26m17s and http://youtu.be/hou2wJCh3XE?t=4m11s
```

### chrome 版本
- https://omahaproxy.appspot.com/
- https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html

- https://chromiumdash.appspot.com/schedule (很清楚，有内核也有对应browser的)
- https://chromestatus.com/roadmap (更新的特性)
### 118的问题
- 有问题

### Chrome Enterprise and Education release notes
- https://support.google.com/chrome/a/answer/7679408?sjid=6136179283723156290-AP
- https://chromereleases.googleblog.com/2023/

