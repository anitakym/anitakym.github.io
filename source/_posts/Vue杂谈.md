---
title: Vue杂谈
date: 2020-05-20 17:16:27
tags:
    - Vue杂谈
    - 工作经验总结系列
---
> 最近招人不太好招，稍微平衡了下标准，具体应用OK的也可，负责的项目以Vue为主，Vue部分会拉着几个官方文档问，比较好做分层

### 2.x我会问的一些问题

- vue-cli 本身这边有xxx-cli,所以看见简历上有写vue-cli的，会分两部，是否有写过 ？ 写过=>具体经验和设计的问题 ： 没有=>拉着文档（https://cli.vuejs.org/zh/guide/plugins-and-presets.html#%E6%8F%92%E4%BB%B6）问一些问题
    - 有没有开发过插件，着重经验和思考（https://cli.vuejs.org/zh/dev-guide/plugin-dev.html）   
    - 更深：对基于插件架构的理解
    - 对于vue-cli的依赖的分析

- vue-router history || hash ，历史模式的话会问一些配置问题，hash模式会问下原理，都蛮有意思的，可拓展性很强；文档（https://router.vuejs.org/zh/guide/essentials/history-mode.html#%E5%90%8E%E7%AB%AF%E9%85%8D%E7%BD%AE%E4%BE%8B%E5%AD%90）

- 跨域问题，着重经验及对此类问题是否有探究和思考（ https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS）聊得有趣的可以更深入了解下计网的基础

- https://cn.vuejs.org/v2/guide/components-edge-cases.html#%E8%AE%BF%E9%97%AE%E5%AD%90%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E6%88%96%E5%AD%90%E5%85%83%E7%B4%A0
文档：
> 这里记录的都是和处理边界情况有关的功能，即一些需要对 Vue 的规则做一些小调整的特殊情况。不过注意这些功能都是有劣势或危险的场景的。我们会在每个案例中注明，所以当你使用每个功能的时候请稍加留意。
代码评审的注意下这部分提到的使用的界限

- 实现一个全选功能，看看对数据驱动思维的理解程度，具体到API层面，可以利用computed（get, set）来实现，还能利用好这个API的缓存优化特性；

- 逻辑完备性 - 条件渲染处理数据有无场景


## retiring 系列
- vue-resource - 可以看看官方发的文章，为什么要retiring it