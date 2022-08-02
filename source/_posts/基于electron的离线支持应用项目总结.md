---
title: 基于electron的离线支持应用项目总结
date: 2021-11-09 18:07:30
tags:
---
### history
> 一个15年的应用，之所以支持离线，是因为校区教室内的网络可能不好，所以需要课中使用时支持离线；

- 那个时候electron的版本和相关构建生态都是比较开始的阶段，基于node的版本也比较低，过了几年，重新起那个项目

```
npm run start
(会发生fse.node无法通过安全与偏好设置，这个需要在安全与偏好设置里面同意一下)

开始错误暂不影响看，可点过掉


● electron-mocha
- https://mochajs.org/
- https://github.com/mochajs/mocha

● electron-prebuilt
  ○ npm地址： https://www.npmjs.com/package/electron-prebuilt
  ○ 说明：electron-prebuilt has been renamed to electron. For more details, see http://electron.atom.io/blog/2016/08/16/npm-install-electron

```
"requires": {
        "electron-download": "^3.0.1",
        "extract-zip": "^1.0.3"
      }
```
被重新命名为electron了（https://www.electronjs.org/blog/npm-install-electron）

● Mac，Windows包(利用两个工具，流程化得进行封包工作)
  ○ appdmg
  ○ rcedit

(基于seal_electron)
● 测试模块
https://www.electronjs.org/spectron
● 构建模块
dps:
electron-log
electron-updater

dev-deps:
electron
electron-builder
electron-webpack
```

### 截屏功能



### electron rebuild
This executable rebuilds native Node.js modules against the version of Node.js that your Electron project is using. This allows you to use native Node.js modules in Electron apps without your system version of Node.js matching exactly (which is often not the case, and sometimes not even possible).
该可执行文件将根据您的Electron项目使用的Node.js版本重建本机Node.js模块。这使您可以在Electron应用程序中使用本机Node.js模块，而无需与系统版本的Node.js完全匹配
- 可配置到script中

### Arch

#### 主进程
- browser window（浏览器窗口，加载网页，注入JSSDK，挂window上面）
- electron updater （客户端更新）
- 客户端监控 - sentry

#### 渲染进程
- JSSDK （暴露给嵌入的页面）


### 功能模块
#### 文件下载
- 网页向客户端提出下载的请求
- 客户端提供了下载的功能，由客户端向服务的请求数据，完成下载，并回调给网页进度和状态
- https://www.electronjs.org/docs/latest/tutorial/process-model#preload-scripts
- JSSDK的注入是通过preload scripts


### 网页端
- babel 是可以配置 electron兼容的
- https://babeljs.io/docs/en/options#targets
"@babel/preset-env",
      {
        "targets": {
          "electron": "9",
        }
      }