---
title: react-intro
date: 2021-04-15 13:30:33
tags:
---
- 参考文档：
https://btholt.github.io/complete-intro-to-react-v5/intro




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