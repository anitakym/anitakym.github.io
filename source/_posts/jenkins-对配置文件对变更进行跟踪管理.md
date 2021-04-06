---
title: jenkins-对配置文件对变更进行跟踪管理
date: 2020-05-07 17:01:40
tags:
    - jenkins&&travis
---

### 先聊聊Jenkins吧
- jenkins pipeline脚本
- 集成打包问题
- CI/CD工具，Jenkins or Gitlab CI/CD or Github CI/CD
- 历史趣事



### 对配置文件对变更进行跟踪管理
Job Configuration History
对配置文件的变更进行跟踪管理

- 安装这个插件：
在manage jenkins => manage plugins里面选择 available ，search Job Configuration History；选择安装并重新启动jenkins即可（PS，会有“仅在没有job的时候重新启动的选项”）

- 使用
在Jenkins=>job config history里面可以查看系统/job的config的变更
也可以在具体的job里面查看当前配置的变更，可以快速回滚配置
具体操作指南可见文档：(https://plugins.jenkins.io/jobConfigHistory/)

### node集成插件
https://plugins.jenkins.io/nodejs/