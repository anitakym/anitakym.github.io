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
```
package.json
包在npm私有仓库中的的完整路径, 指明tgz包的版本，安装指定版本的npm包
  "_resolved": "http:/xxx/repository/npmjs.org/xxxx/-/xxxx-1.1.9.tgz",
也就是包_resolved字段里面那个值，我们发布了包之后，在管理端也能看到地址

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


### nexus部署服务器磁盘空间不够处理

1. 可以在Blob Stores里面看下磁盘占用情况，确认占用多的是哪些类型（jar or npm包 ？）
2. 配置cleanup policies，在设置按钮的 Repository-Cleanup Polices选项下，选择 +Create Cleanup Policy，然后配置一个你认为没问题的策略，这个里面还可以preview，看看这个策略下，哪些会被删除；
3. 进入Repository里面，根据1确认的 repositry，点击进去，在settings里面，修改Cleanup选项，刚刚配置的策略添加到applied里面即可；
4. 点击system-tasks,点击 +Create task(type Admin-compact blob store)，可以选择手动触发，然后手动run一下，即进入清理模式；这个时候可以通过状态判断是否清理完成，我这边100多个G，大概running了1个多小时快2个小时才跑完；

#### error
```
javax.servlet.ServletException: com.orientechnologies.orient.core.exception.OLowDiskSpaceException: Error occurred while executing a write operation to database 'component' due to limited free space on the disk (3898 MB). The database is now working in read-only mode. Please close the database (or stop OrientDB), make room on your hard drive and then reopen the database. The minimal required space is 4096 MB. Required space is now set to 4096MB (you can change it by setting parameter storage.diskCache.diskFreeSpaceLimit) . DB name="component"
```
- 跑task清理
- {安装目录}/bin/nexus.vmoptions - storage.diskCache.diskFreeSpaceLimit = 2048


### nexus文档指路（sonatype）
#### repository manager(注意根据自己搭建的版本选择文档)
- https://guides.sonatype.com/repo3/quick-start-guides/proxying-maven-and-npm/
- https://help.sonatype.com/repomanager3
- https://help.sonatype.com/repomanager2

