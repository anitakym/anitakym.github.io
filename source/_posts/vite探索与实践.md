---
title: vite探索与实践
date: 2022-09-09 16:19:09
tags:
---
https://www.yuque.com/vueconf/mkwv0c/ud1un9

#### 依赖预构建 - 开发环境
- .vite 目录下

### others
#### vite-node
- Vite as Node runtime.
- The engine powers Vitest and Nuxt 3 Dev SSR.

### plugin-legacy
- https://polyfill.io/v3/packages
- https://polyfill.io/v3/url-builder
```
modernPolyfills
Type: boolean | string[]

Default: false

Defaults to false. Enabling this option will generate a separate polyfills chunk for the modern build (targeting browsers with native ESM support).

Set to a list of strings to explicitly control which polyfills to include. See Polyfill Specifiers for details.

Note it is not recommended to use the true value (which uses auto-detection) because core-js@3 is very aggressive in polyfill inclusions due to all the bleeding edge features it supports. Even when targeting native ESM support, it injects 15kb of polyfills!

If you don't have hard reliance on bleeding edge runtime features, it is not that hard to avoid having to use polyfills in the modern build altogether. Alternatively, consider using an on-demand service like Polyfill.io to only inject necessary polyfills based on actual browser user-agents (most modern browsers will need nothing!).
```
### vite 升级问题
- https://v2.vitejs.dev/guide/migration.html
- 1.8.4 有polyfill标准的问题 - 改成 proposalshipped
- https://cn.vitejs.dev/config/build-options.html
- https://github.com/vitejs/vite/issues/9794

### 更新-持续中
Vite 5.2 is out! ⚡️
🔐 CSP nonce and require-trusted-types-for support
🧩 import.meta.filename/dirname support in SSR
🧙‍♂️ shiki+twoslash powered code snippets in docs
⏩ Update to esbuild 0.20
🛠️ Significant fixes across the board