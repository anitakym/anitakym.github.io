---
title: open-source-开源-study
date: 2021-04-04 16:19:44
tags:
---
### 推荐站点
https://snyk.io/advisor/

### Workshop
- https://slides.com/kentcdodds/write-oss
- 有如何写一个open source software 相关资源
### CI(持续继承)
- https://www.travis-ci.org/
- circleci.com

#### 提交(precommmit,aftercommit)
#### 构建部署（Jenkins，travis-ci）
#### 测试（构建前-单测，构建后-功能）
#### 版本控制（新增，备份，回滚）

### 单测
- 覆盖率
codecov.io
coveralls.io

### 文档
github.io
gitee.io（网络问题，可以作为镜像站点试试）
www.netlify.com
vuepress

### issue （bug or feature需求）
- 让用户按照模版提issue
- 利用插件提高issue管理效率：
  - github.com/apps/close-issue-app
  - issue-helper
    - https://github.com/vuejs/vue-issue-helper
    - (https://vuecomponent.github.io/issue-helper/?lang=zh)——ant-design-vue提供的提issue的模版界面
  - https://github.com/dessant/lock-threads —— 锁死不活跃的issue，用户不能再回复了


### 前端开源项目分类
  - CMS/blog Framework (hexo, ghost)
  - JavaScript Library/Framework (vue, react, jquery)
  - Plugin (bootstrap, vuex, vue-router)
  - utility(lodash, commander.js, underscore)

### 自由软件（若为自由故）

### 项目结构组织
#### 授权协议 
- LGPL/GPL/BSD/MIT/Apache

#### 环境
> 让开发者能快速上手
> 提供docker环境
- 开发者环境
- 依赖环境
- 部署环境

#### Example
类似于ElementUI，example就很完整全面
- API演示
- 扩展演示
- 基本用法/高级用法

#### 版本控制
开发/Beta/Release
详细可见博文：软件版本

#### 社区
- bug反馈
- 特性讨论
- 扩展插件

#### 自动集成
- 自动部署
- 自动测试
- 环境检查
- 跨浏览器测试

#### 构建
> 脚本 + 这一套工具也需要开放给开发者
- 编译工具
- 冗余文件清理
- 格式化
- 版本文档更新
- 合并压缩优化
- 发布

#### 文档
- API说明
- README
- 多语言支持
- 快速上手
- 最佳实践
- 开发者文档
- 注释doc工具
  

#### 源码
- 模块组织方式
- 代码规范 - code of conduct
- 提交格式
- 语法检查 - lint工具

#### 测试
- 命令行测试
- 浏览器测试
- 测试覆盖率

### 结构设计原则

#### 分离原则
- 源码
- 调试编译-debug
- 编译部署

#### 子系统
- git submodule
- 包管理工具
- 协助分组（organization，child project）
```
/ 下载子模块
$ git submodule update --init --recursive
```
```
.gitmodules
[submodule "XXXX"]
	path = XXXX
	url = https://github.com/xxx/XXXX.git
```



### 推广
#### 官网
- 在线站点
- 友情链接赞助

#### 论坛社区
- BBS
- 问答社区

### 解决反馈和处理PR


#### 技术会议

#### 文档沉淀
- wiki/issues/pages

#### blog/专栏

#### 投稿
公众号/技术社区