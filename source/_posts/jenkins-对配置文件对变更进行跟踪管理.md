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


#### 参数化构建
- git parameter
给git可选参数
- choice parameter
比如传入一些构建时需要的参数

上面两个都需要下载对应的插件

#### node环境
- nodejs插件：
在插件管理面搜nodejs,安装即可（https://plugins.jenkins.io/nodejs/）

- 在系统管理->全局工具配置->nodejs
新建一个nodejs环境

- Provide Node & npm bin/ folder to PATH
选择node版本
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

### 拓展
#### JenkinsX
https://jenkins-x.io/docs/reference/pipeline-syntax-reference/


#### Android
- active choices reactive parameter
- groovy script

#### job配置的导出导入
- https://wiki.jenkins.io/display/JENKINS/Administering+Jenkins#AdministeringJenkins-Moving/copying/renamingjobs
- 同Jenkins可以直接copy from
 - jenkins-cli.jar
 - https://www.jenkins.io/doc/book/managing/cli/
 ```
 # manage jenkins | jenkins-cli | get-job
 java -jar jenkins-cli.jar -s 【domain】 -auth 【account】:【pwd】 get-job 【job name】> 【job name】.xml
 ```
 ```
➜  Downloads java -jar jenkins-cli.jar -s http://xxxxxx:xxxx/ -auth xxxxxx:1234 get-job seal-troy-frontend > seal-troy-frontend.xml
➜  Downloads code seal-troy-frontend.xml 
➜  Downloads java -jar jenkins-cli.jar -s http://xxxxxx:xxxx/ -auth xxxxxx:1234 create-job seal-troy-frontend-copy < seal-troy-frontend.xml
 ```
 
 #### jenkins 版本的升级和回退需要注意
 因为插件是依赖于Jenkins的版本的，所以如果回退Jenkins版本，可能会导致依赖于更高版本的已装插件的不可用；
 - case ，multijob插件，然后基于这个创建了一个jobA, Jenkins版本被回退到不支持multijob的版本，这个时候，表现为 jobA无法搜索到，但是去服务器上面查，能查到项目的workspace和jobs的配置文件，拿着xml配置文件create-job的时候，
 ```
 ERROR: Unexpected exception occurred while performing create-job command.
com.thoughtworks.xstream.mapper.CannotResolveClassException: com.tikal.jenkins.plugins.multijob.MultiJobProject
 ```
 就发现，哦multijob这儿出问题
 ```
 This plugin is a MultiJob plugin.
Warning: This plugin has dependencies on other plugins that require Jenkins 2.289.1 or newer. Jenkins will refuse to load the dependencies requiring a newer version of Jenkins, and in turn loading this plugin will fail.
 ```