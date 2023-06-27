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

### 关注API的变化
- https://github.com/getsentry/sentry-javascript/blob/7.47.0/MIGRATION.md/#remove-requirement-for-sentrytracing-package-since-7460

### @sentry/vue
相比于 `@sentry/browser`，`@sentry/vue` 专为 Vue.js 应用程序量身定制，提供了更好的 Vue.js 集成和错误跟踪。以下是 `@sentry/vue` 相对于 `@sentry/browser` 的一些优势：

1. Vue 错误处理器

`@sentry/vue` 提供了一个全局的 Vue 错误处理器，会自动捕获并报告 Vue.js 的渲染错误、生命周期错误和自定义方法中的错误。这意味着您无需手动在组件内部捕获和报告错误。

2. Vue 插件集成

`@sentry/vue` 作为一个插件可以轻松地集成到 Vue 应用程序中。在配置时，只需传入您的 Sentry DSN（数据来源名称），插件就会自动捕获和报告错误。

示例配置:

```javascript
import Vue from 'vue';
import * as Sentry from '@sentry/vue';
import { Integrations } from '@sentry/tracing';

Sentry.init({
  Vue: Vue,
  dsn: 'your_sentry_dsn',
  integrations: [
    new Integrations.BrowserTracing(),
  ],
  tracingOptions: {
    trackComponents: true, // 追踪 Vue 组件性能
  },
});
```

3. Vue.js 上下文信息

错误报告中的上下文信息对于调试非常重要。 `@sentry/vue` 会自动为每个错误报告附加与 Vue 组件相关的附加信息（例如，组件名称，组件层次结构等）。这使得错误报告更有上下文，方便您快速排查问题。

4. Vue.js 性能追踪

`@sentry/vue` 提供了 Vue.js 组件性能追踪功能。通过轻松配置，Sentry 可以追踪和测量组件性能，帮助您了解每个组件的渲染时间和性能瓶颈。

简而言之，`@sentry/vue` 在 `@sentry/browser` 的基础上，提供了适用于 Vue.js 应用程序的专有功能，使得错误报告更加详细和有用。使用 `@sentry/vue`，您可以轻松地集成 Sentry 到 Vue 应用中，实现准确的错误追踪和性能分析。

#### vendor/components.ts
- https://github.com/vuejs/vue/blob/612fb89547711cacb030a3893a0065b785802860/src/core/util/debug.js
- // Vendored from https://github.com/vuejs/vue/blob/612fb89547711cacb030a3893a0065b785802860/src/core/util/debug.js
- // with types only changes.


### @sentry/react\
在 `@sentry/browser` 的基础上，`@sentry/react` 提供了为 React 应用程序量身定制的附加错误处理和性能跟踪功能。以下是相比于 `@sentry/browser`，`@sentry/react` 中提供的一些重要增强功能：

1. **错误边界（ErrorBoundary）**：用于捕获 React 组件树中未捕获的错误。通过使用 `withErrorBoundary` 高阶组件（HOC）或 `<ErrorBoundary>` 组件包装 React 组件，可以捕获组件发生的错误，并将它们自动地报告给 Sentry。

2. **性能跟踪**： `@sentry/react` 为 React 应用提供了特定的性能跟踪工具，用于更细粒度地测量组件性能。在 React 应用程序中，`@sentry/react` 自动为普通的 React 组件测量渲染性能。你只需在应用程序中包含 `@sentry/react` 插件即可。此外，`@sentry/react` 还提供了用于手动测量性能的工具，例如：`withProfiler` 高阶组件（HOC）和 `<Profiler>` 组件。

3. **集成**： `@sentry/react` 包含了一些与开发环境的 React 扩展的集成。例如，`@sentry/react` 自动与 `create-react-app` 进行了集成，以方便地构建和部署错误报告和性能跟踪功能。

下面是一个简单的错误边界示例：

```javascript
import React from 'react';
import { withErrorBoundary } from '@sentry/react';

const MyComponent = () => {
  // Your component logic...
};

export default withErrorBoundary(MyComponent, {
  fallback: <div>Oops! An error occurred.</div>,
  showDialog: true,
});
```

这片代码在 React 组件中引入了错误边界，当组件发生错误时，会自动报告给 Sentry 并显示一个默认的降级 UI。