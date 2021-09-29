---
title: sentry实践
date: 2021-04-12 17:23:06
tags:
---

### 部署

#### sentry 私有化部署

1.使用 docker 做私有化部署，依赖于官方的（https://github.com/getsentry/onpremise）
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

sentry 目录下 ——

config.yml
sentry.conf.py
.env w/ environment variables

config.example.yml ——

如要修改时区

```
docker ps
locate sentry.conf
vim sentry.conf.py
增加 SENTRY_DEFAULT_TIME_ZONE = 'Asia/Shanghai'
docker restart sentry_onpremise_web_1
```

# Mail Server

这里面需要申请一个公司的邮箱，配置到 mail.username 里面

# System Settings

system.internal-url-prefix: '申请个外网域名'
system.url-prefix: '同上'

requirements.example.txt ——
如果需要集成 dingding,可以在这个里面添加 plugin
(https://github.com/anshengme/sentry-dingding)

#### 私有化部署的几个小坑

- 推荐阅读案例：https://segmentfault.com/a/1190000038839629 ， https://xupeiyao.github.io/2020/01/24/deploy_sentry/

1. 及时关注修复的 bug
   https://github.com/getsentry/onpremise/issues/635

比如 10 年上半年部署的项目，查出来，如果修改了 nginx/nginx.conf 里面的配置的

```
	log_format main '$remote_addr - $remote_user [$time_local] "$request" '
	'$status $body_bytes_sent "$http_referer" '
	'"$http_user_agent" "$http_x_forwarded_for"';
```

查 docker logs 的时候，并不会有新增的 x_forwarded_for 的输出（如果 nginx.conf 里面写了会导致报错的配置，报错是立刻的）
需要再加下

```
	access_log /var/log/nginx/access.log main;
```

官方文档参考：http://nginx.org/en/docs/http/ngx_http_log_module.html

2.取真实 IP，需要在部署的 sentry.xxx.xx.cn 的 nginx 里面，增加对信息的透传

```
proxy_set_header X-Forwarded-Proto  $scheme;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
```

3.部署的 onpremise，查各种问题，日志就可以用 docker 了

```
docker ps
docker inspect
docker restart
```

### 项目应用

#### 文档指南

https://docs.sentry.io/

#### sourcemap 上传

sentry 上传 sourcemap 配置

- 可以用@sentry/webpack-plugin
- sentry cli(https://docs.sentry.io/platforms/javascript/sourcemaps/uploading/)

#### web 项目

- @sentry/browser
- @sentry/integrations 如果是 Vue 项目

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

不同版本的 sentry 也提供了不同的方式，按照文档说明选择和更新即可

- sourcemap 上传配置

#### electron 项目

- @sentry/electron(https://docs.sentry.io/platforms/javascript/guides/electron/)
  - @sentry/electron is the official Sentry SDK for Electron applications. It can capture JavaScript exceptions in the main process and renderers, as well as collect native crash reports (Minidumps).
  - 可以捕获主进程和渲染器中的 JavaScript 异常，也可以收集本地崩溃报告（Minidumps）。
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

前置：需要在管理后台配置 sentry 的域名

开源封装的库：

- https://github.com/lizhiyao/sentry-miniapp

- https://github.com/youzan/raven-weapp

### 基本操作

DSN 查询：
project => settings => client keys

1.定义日志异常上报方法 2.区分环境（开发，测试，生产）

## 问题处理
### Vue

```
# 这段如果不加的话，写在.Vue文件里面的错误，就抛不到sentry上；但是写在.js文件里面抛的错误能到sentry上
  Vue.config.errorHandler = err => {
    Sentry.captureException(err)
  }
```

### Flutter
- 调试不要用ios模拟器，网络上面不会请求也不会报错
    - 解决网络问题：Mac的网络偏好设置-->高级-->代理-->把网页代理和安全网页代理前面的勾去掉
- andriod调试网络没有问题，可以直接调试
- 真机调试，允许网络(局域网+蜂窝)+查找并连接到本地的网络设备（好），就可以了
- https - DSN
- 确保sentry初始化走通了