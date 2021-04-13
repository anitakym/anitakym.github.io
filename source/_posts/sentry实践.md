---
title: sentry实践
date: 2021-04-12 17:23:06
tags:
---
### 部署
sentry 私有化部署

1.使用docker做私有化部署，依赖于官方的（https://github.com/getsentry/onpremise）
Official bootstrap for running your own Sentry with Docker.

2.环境需求：
Docker 19.03.6+
Compose 1.24.1+
4 CPU Cores
8 GB RAM
20 GB Free Disk Space

3.具体操作可见官方文档：https://github.com/getsentry/onpremise
简单一句话：如果使用默认值的配置，只需要克隆项目，然后在本地运行 ./install.sh 就可以了

4.具体配置：The recommended way to customize your configuration is using the files below, in that order:

sentry目录下 —— 

config.yml
sentry.conf.py
.env w/ environment variables

config.example.yml —— 
# Mail Server #
这里面需要申请一个公司的邮箱，配置到mail.username里面
# System Settings #
system.internal-url-prefix: '申请个外网域名'
system.url-prefix: '同上'

requirements.example.txt ——
如果需要集成dingding,可以在这个里面添加plugin
(https://github.com/anshengme/sentry-dingding)

### 项目应用


#### sourcemap 上传
sentry 上传sourcemap 配置
- 可以用@sentry/webpack-plugin
- sentry cli(https://docs.sentry.io/platforms/javascript/sourcemaps/uploading/)


#### web项目
- @sentry/browser
- @sentry/integrations 如果是Vue项目
```
import * as Sentry from '@sentry/browser'
import * as Integrations from '@sentry/integrations'
Sentry.init({
  release: ,
  environment: ,
  dsn: "",
  integrations: [new Integrations.Vue({
      Vue,
      attachProps: true
    })]
})
```

+ sourcemap上传配置


#### electron项目

- @sentry/electron(https://docs.sentry.io/platforms/javascript/guides/electron/)
  - @sentry/electron is the official Sentry SDK for Electron applications. It can capture JavaScript exceptions in the main process and renderers, as well as collect native crash reports (Minidumps).
  - 可以捕获主进程和渲染器中的JavaScript异常，也可以收集本地崩溃报告（Minidumps）。
- crashReporter
```
import * as Sentry from '@sentry/electron';
import { crashReporter } from 'electron';
Sentry.init({ dsn: '' });
crashReporter.start({
        companyName: '',
        submitURL: 'sentry的',
        uploadToServer: true,
        ignoreSystemCrashHandler: true
    });
```


#### 小程序原生项目
前置：需要在管理后台配置sentry的域名

开源封装的库：
- https://github.com/lizhiyao/sentry-miniapp

- https://github.com/youzan/raven-weapp