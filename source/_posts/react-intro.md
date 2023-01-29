---
title: react-intro
date: 2021-04-15 13:30:33
tags:
---
- 参考文档：
https://btholt.github.io/complete-intro-to-react-v4/
https://btholt.github.io/complete-intro-to-react-v5/

## basic
- 声明式UI，组件化
- 解决应用的主要问题|用户界面的问题（工作量）
- 2015.8 - facebook F8
- react - UI库
- 定义（代码偏向声明式）一次用户界面，用在多个地方
- 状态（state） => 自动反应，更新界面
- 只维护应用的状态

## 实践项目中遇到的一些问题
> 因为react相关项目是另外一个组负责，组间评审的时候，会看下项目，下面为遇到的一些问题
### creat-react-app
https://github.com/facebook/create-react-app/issues/10161
关于eslintcache文件产生的位置问题(4.0.1)

eslint --cache false可以本地起效，但是不是解决方案

move .eslintcache into node_modules/.cache
https://github.com/facebook/create-react-app/pull/10346
react team 的哥们回复
https://github.com/facebook/create-react-app/pull/9977



eslint: {
    cache: false,
  },

4.0.2


to ignore a file already tracked you also need to run git rm --cached .eslintcache
gitignore


### 修改PORT，HOST
直接
.env
PORT = 3003
HOST = '127.0.0.1'


## Framework
### ice
- 可视化页面构建
- https://github.com/alibaba/ice
- 时效性较强页面
- 后端路由服务
- 产出 - 当前布局与内容的DSL（JSON）
- 组件间的通信 - 将不同组件通过自定义的钩子hook起来
```
class FetchData extends Components {
  state = {
    data: {},
  }
  componentDidMount() {
    const { componentApi } = this.props
    api.get(componentApi)
      .then((response) => {
        this.setState({
          data: response,
        })
      })
  }
  render() {
    return <WrappedComponent {..props} data={this.state.data} />
  }
}
```
## lazy loadable
React.lazy and Suspense are not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we recommend Loadable Components. It has a nice guide for bundle splitting with server-side rendering.

## stric mode
- Suggested: We strongly suggest you enable Strict Mode in your Next.js application to better prepare your application for the future of React.
- 还是建议使用的，如果是新项目的话，能更好的适应React后续的发展
- 16.3引入的，且对生产环境毫无影响，能在console中打印有用的警告信息
- https://github.com/facebook/react/issues/17786 - 一个有意思的issue


## reportWebVitals
- web-vitals
- https://www.npmjs.com/package/web-vitals
- https://zhuanlan.zhihu.com/p/149662237
- https://blog.chromium.org/2020/05/introducing-web-vitals-essential-metrics.html
- essential metrics for a healthy site
- https://create-react-app.dev/docs/measuring-performance/

### conf
```
React conf 2018

Sophie Alpert

1.25M developer

Renewable energy

Make it easier to build great UIs.

Code splitting

1.simplify hard stuff(suspense)
2.performance(time slicing)
2.developer tooling(profiler)

What still sucks
Reusing logic--Wrapper hell
Giant components
Confusing classes(hard for humans,machines,hot roloading)
```

#### readings
- https://blog.oyanglul.us/javascript/react-cookbook-mini
- https://blog.oyanglul.us/javascript/understand-prototype