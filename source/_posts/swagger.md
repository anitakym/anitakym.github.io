---
title: swagger
date: 2021-06-22 15:13:04
tags:
---
### 接口文档：
详细地描述了后端接口的访问方式和参数说明

### 接口定义方式主要有两种：
- Swagger等，RESTFUL API；
- protobuf，跨语言的接口定义；
  - （https://github.com/protocolbuffers/protobuf/tree/master/java）
  - （https://developers.google.com/protocol-buffers/）
  -  （https://opensource.com/article/19/10/protobuf-data-interchange）

### 推荐阅读：
https://swagger.io/
https://swagger.io/tools/open-source/

swagger：
#### history
- SmartBear Software
- RESTFUL API工具
- 设计，构建，记录，使用
- openAPI Initiative

#### uses
- 项目中接口展现
- 接口更新
- 直接接口调用


### 目前团队使用的API-Management工具——YAPI
#### EasyYapi - 可以导出http,rpc，call api 调用 API
- Java端用：http://easyyapi.com/documents/index.html
- https://github.com/tangcent/easy-yapi/blob/master/README.md
- 对代码0入侵
- （https://github.com/diwand/YapiIdeaUploadPlugin/wiki/%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8）可做替代
- IDEA插件

#### apimock
swaggerconfig配置类集成到 api-mock组件中，swagger生成的接口文件可以通过数据导入，导入到yapi中

### 其他
- https://github.com/thx/rap2-delos 阿里妈妈出品，开源接口管理工具
  - 接口文档管理
  - Mock
  - 导出