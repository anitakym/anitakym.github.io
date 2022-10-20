---
title: evan_22_web_trend_frontend_summary
date: 2022-10-19 14:47:53
tags:
---
- https://juejin.cn/book/7127092198096502822/section/7127210360884428812
> evan
## 讲稿笔记
> 以下内容均为讲稿笔记
### 开发范式&底层框架
#### React Hooks
- 已经彻底取代了Class Components
- 启发了组件逻辑表达和逻辑复用的新范式
- Vue Composition API | Sevelte | SolidJS

#### React Hooks的开发体验问题逐渐被正视
- Hooks执行原理和原生JS心智模型的差异
- 不能条件式调用
- Stale Closure（过期闭包）的心智负担
- 必须手动声明useEffect依赖
- 如何“正确”使用useEffect是个复杂的问题
- 需要useMemo / useCallback等手动优化

#### React 团队对改善开发体验的努力
- useEvent RFC改善
- useCallback 的问题
- Dan Abramov花大量时间改进新版useEffect文档
- 黄玄正在开发中的React Forget意再避免需要手动声明依赖

#### 基于依赖追踪的范式重新得到重视
- SolidJS ｜ Vue Composition API | Ember Starbeam
- https://github.com/starbeamjs/starbeam
- 共同点：一次调用，符合原生JS直觉；自动追踪依赖，无需手动声明；引用稳定，无需useCallback

#### 基于编译的响应式系统
- Svelte ｜ Vue Reactivity Transform | solid-labels
- Svelte简洁的代价：只能在Svelte组件内使用｜组件外需要不同的API｜只能在顶层作用域使用，不可在函数体内使用
- Vue Reactivity Transform | solid-labels ： 可在组件和普通JS/TS文件中使用

#### 统一模型的优势和代价
- 优势：利于长期的重构和服用
- 代价：底层实现的抽象泄漏，初期的学习成本

#### 基于编译的运行时优化
- Svelte｜ Solid ｜ Vue Vapor Mode
- 不同策略对生成代码量的影响（组件数量/打包后总大小）

### 工具链
#### 原生语言再前端工具链中的使用
- esbuild(Go)
- SWC(Rust)
- Bun(Zig)
- Parcel 2 (JS/Rust hybrid)
- Vite(JS/ Go hybrid via esbuild)
- napi-rs(Rust)

#### 原生语言在前端工具链中的使用
- 原生语言更适用于用例专注且标准相对稳定的情况，否则很难榨取最大化的性能优势
- 原生语言会影响可扩展性，增加社区参与门槛，影响生态发展
- JS/原生混合工具链将会成为常态

#### 工具链的抽象层次
- 专注于打包，抽象层次低 - browserify | webpack | rollup
- 专注于应用，抽象层次高 - parcel ｜ vue-cli | cra
- cli专注于应用，抽象层次高；API专注于支持上层框架，抽象层次中 - vite

#### 基于Vite的上层框架
- Nuxt3 | SvelteKit | Shopify Hydrogen | Astro | Qwik | FastifyDX | Solid Start | Laravel新默认前端方案

### 上层框架Meta Frameworks
> 一个语言，前后“打通”
#### 数据的前后打通
- Next - getStaticProps/getServerSideProps
- Nuxt - API routes + useFeth + top level await
- Remix loader/action + enhanced HTML Form

- 通过显式引入共享类型
- 自动基于DB schema生成类型
- Nuxt3 自动基于文件布局生成API/路由类型

#### 全栈的代价
- 虽然数据已经渲染出了HTML，但还是需要额外发送一份数据用于Hydrate
- 即使在客户端没有交互的组件依然会被打包发送至用户端
- Hydrate 影响页面交互指标（TTI）

#### 社区的探索方向
- Server-only Components（Hydrogen, Next, Nuxt）
- Partial hydration / Island Architecture (Astro, Isles, Fresh)
- Fine-grained + resumable hydration (Owik)
- Shell + partial hydration (VitePress)
