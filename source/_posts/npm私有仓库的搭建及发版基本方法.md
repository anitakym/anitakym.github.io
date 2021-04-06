---
title: npm私有仓库的搭建及发版基本方法
date: 2020-04-13 17:02:58
tags:
    - 工作经验总结系列
---

> 让运维老师帮忙用Nexus搭了我们NPM私仓库，严格说，给我们提供了NPM的支持

私仓——使用需要配置源，个人电脑使用推荐nrm

## 私仓的使用

#### 源的配置
写到脚本里面：
```
npm --registry http://xxxxx/repository/npmjs.org/
"setup": "npm install --force --registry http://xxxxx/repository/npmjs.org",
```
设置全局：
```
npm help config // 查询config具体用法
npm config set registry http://xxxxx/repository/npmjs.org/
npm config get registry
```

#### nrm
文档指路：https://www.npmjs.com/package/nr

#### nexus配置
获取包的源和发布包的源可以在nexus里面配置

#### 发包版本控制
tips: 注意正式版本和发测试版本包的时候，发包规则的设定，可以用npm publish --tags=beta来发测试版本


## 私仓的搭建（基于nexus）



### npm发包
1.注册账号
2.package.json (name,version=>最少字段)
3.main/module/files-需要发布的本地目录/


tips:
1.发npm包时候，源就是npm的;注意publish的源的设置
2.推荐工具：nrm
3.keyword方便搜索的

