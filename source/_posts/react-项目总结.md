---
title: react-项目总结
date: 2023-02-16 11:46:21
tags:
---
#### why
- 交互式UI-简单
- 组件化
- 跨平台

#### history - feature
`https://github.com/facebook/react/releases`
- v16.0 - 2017.09 
```
重写Reconciler - 性能，Fiber - 性能 ，createPortal API - 让节点渲染到指定容器内，更好实现弹窗功能 ，componentDidCatch -> 划分了错误边界，捕获渲染中的异常
```
- v16.2
```
React
Add Fragment as named export to React. (@clemmy in #10783) -> 解决数组元素问题
Support experimental Call/Return types in React.Children utilities. (@MatteoVH in #11422)

```
- v16.3
```
React
Add a new officially supported context API. (@acdlite in #11818)
Add a new React.createRef() API as an ergonomic alternative to callback refs. (@trueadm in #12162)
Add a new React.forwardRef() API to let components forward their refs to a child. (@bvaughn in #12346)
Fix a false positive warning in IE11 when using React.Fragment. (@XaveScor in #11823)
Replace React.unstable_AsyncComponent with React.unstable_AsyncMode. (@acdlite in #12117)
Improve the error message when calling setState() on an unmounted component. (@sophiebits in #12347)
```
- v16.6
```
React
Add React.memo() as an alternative to PureComponent for functions. (@acdlite in #13748) - 控制子组件的渲染
Add React.lazy() for code splitting components. (@acdlite in #13885) - 代码分割
React.StrictMode now warns about legacy context API. (@bvaughn in #13760)
React.StrictMode now warns about findDOMNode. (@sebmarkbage in #13841)
Rename unstable_AsyncMode to unstable_ConcurrentMode. (@trueadm in #13732)
Rename unstable_Placeholder to Suspense, and delayMs to maxDuration. (@gaearon in #13799 and @sebmarkbage in #13922)
React DOM
Add contextType as a more ergonomic way to subscribe to context from a class. (@bvaughn in #13728) - 方便类组件使用context
```
- v16.8 - Add Hooks — a way to use state and other React features without writing a class. (@acdlite et al. in #13968) - 使函数组件也能做类组件做的一切事儿
- v17 - 2020.10 - 事件绑定（document -> container ）, 移除事件池
`https://reactjs.org/blog/2020/10/20/react-v17.html`


#### react-scripts
- https://www.npmjs.com/package/react-scripts
- @svgr/webpack
```
This package includes scripts and configuration used by Create React App.
Please refer to its documentation:
```

#### better-scroll
```
BetterScroll 是一款重点解决移动端（已支持 PC）各种滚动场景需求的插件。它的核心是借鉴的 [iscroll](https://github.com/cubiq/iscroll) 的实现，它的 API 设计基本兼容 iscroll，在 iscroll 的基础上又扩展了一些 feature 以及做了一些性能优化。

BetterScroll 是使用纯 JavaScript 实现的，这意味着它是无依赖的。
```
- https://github.com/ustbhuangyi/better-scroll


#### react-lazyload

#### react-flow
- https://github.com/wbkd/react-flow
- 高度可定制的库，用于构建基于节点的交互式用户界面、工作流程编辑器、流程图或静态图

#### react-transition-group

#### @emotion/react
Emotion is a library designed for writing css styles with JavaScript. It provides powerful and predictable style composition in addition to a great developer experience with features such as source maps, labels, and testing utilities. Both string and object styles are supported.

#### JavaScript Glob 匹配器 - minimatch

##### 什么是 Glob 模式
Glob 是一种文件路径匹配模式，源自 Unix shell，用通配符来匹配文件名：
- `*` - 匹配任意数量字符（除了路径分隔符）
- `**` - 匹配任意数量目录层级
- `?` - 匹配单个字符
- `[abc]` - 匹配括号内任一字符
- `{a,b,c}` - 匹配大括号内任一选项

##### minimatch 库的作用
minimatch (https://isaacs.github.io/minimatch/) 是一个纯 JavaScript 实现的 glob 匹配器，核心功能：

```javascript
const minimatch = require('minimatch')

// 基础匹配
minimatch('foo.js', '*.js')        // true
minimatch('foo/bar.js', 'foo/*.js') // true
minimatch('foo/bar/baz.js', '**/baz.js') // true

// 复杂模式
minimatch('foo.test.js', '*.{js,ts}') // true
minimatch('src/components/Button.tsx', 'src/**/*.{js,jsx,ts,tsx}') // true
```

##### 为什么有如此多引用

**1. 构建工具生态系统**
- **Webpack**: 用于 entry 配置、文件过滤
- **Rollup**: bundle 分析与 tree-shaking
- **Vite**: 静态资源处理与热更新
- **ESLint**: 配置文件的 ignore patterns
- **Prettier**: 格式化文件过滤
- **Jest/Vitest**: 测试文件匹配

**2. Node.js 工具链依赖**
- **npm/yarn**: package.json 的 files 字段
- **glob** 包: Node.js 最流行的文件匹配库，内部使用 minimatch
- **fast-glob**: 高性能文件匹配，也依赖 minimatch 语法
- **chokidar**: 文件监听器，用于路径过滤

**3. 框架与脚手架**
- **Create React App**: 构建配置与文件处理
- **Next.js**: 页面路由匹配
- **Nuxt.js**: 静态文件处理
- **Angular CLI**: 项目文件管理

**4. CI/CD 与部署**
- **GitHub Actions**: workflow 文件路径匹配
- **GitLab CI**: 触发条件配置
- **Docker**: .dockerignore 模式匹配

##### 实际应用场景

**文件批处理:**
```javascript
const glob = require('glob')
const minimatch = require('minimatch')

// 匹配所有测试文件
const testFiles = glob.sync('src/**/*.{test,spec}.{js,ts}')

// 过滤特定模式
const componentFiles = files.filter(file => 
  minimatch(file, 'src/components/**/*.{tsx,jsx}')
)
```

**配置文件使用:**
```json
// .eslintrc.js
{
  "ignorePatterns": [
    "dist/**/*",
    "node_modules/**/*",
    "**/*.d.ts"
  ]
}

// jest.config.js
{
  "testMatch": [
    "**/__tests__/**/*.(js|jsx|ts|tsx)",
    "**/*.(test|spec).(js|jsx|ts|tsx)"
  ]
}
```

##### 性能与优化
- **编译缓存**: minimatch 可将 glob 模式编译为正则表达式并缓存
- **最小化匹配**: 避免过于宽泛的模式（如单独的 `**`）
- **早期退出**: 利用路径前缀快速排除不匹配项

##### 总结
minimatch 成为 JavaScript 生态系统基础设施的原因：
1. **标准化**: 统一了各工具的文件匹配语法
2. **可靠性**: 经过大量实际项目验证
3. **性能**: 高效的匹配算法实现  
4. **兼容性**: 与 Unix shell glob 语法兼容
5. **无依赖**: 纯 JavaScript 实现，易于集成

这解释了为什么几乎所有主流 JavaScript 构建工具、测试框架、代码检查工具都直接或间接依赖 minimatch。


## 优化
