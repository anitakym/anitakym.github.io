---
title: maven
date: 2021-08-30 11:37:30
tags:
---

### 文档指路

https://maven.apache.org/

### 概述

“Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.”

### 构建工具，依赖管理
maven排在Java生态的第一，Gradle用于Android
#### 基于XML格式的文件描述依赖配置
- https://maven.apache.org/pom.html#What_is_the_POM
- POM（Project Object Model）
- pom.xml 
  - groupId,artifactId,version - 坐标
  - type - 类型
  - scope - 范围
  - optional - 依赖是否可选
  - exclusions - 排除传递性依赖

#### 依赖仲裁原则
- 最短路径优先
- 第一声明有限


### Best Practice
- 减少重复配置的代码
- 减少不确定因素

### 问题解决
- 确认系统，确认Java，Maven版本
- 确认本地依赖的缓存
- 检查完整依赖树

### 推荐插件
- http://maven.apache.org/enforcer/maven-enforcer-plugin/
### 关于私仓
- 可见这篇文章（也是基于nexus构建的）：http://www.imaginingme.cn/2020/04/13/npm%E7%A7%81%E6%9C%89%E4%BB%93%E5%BA%93%E7%9A%84%E6%90%AD%E5%BB%BA%E5%8F%8A%E5%8F%91%E7%89%88%E5%9F%BA%E6%9C%AC%E6%96%B9%E6%B3%95/