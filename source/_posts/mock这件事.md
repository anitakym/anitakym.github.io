---
title: mock这件事
date: 2021-11-02 16:09:10
tags:
---

### mockjs
#### 语法规范
- 数据模版定义 DTD
- 数据占位符定义 DPD
  - 占位符：只在属性字符串中占个位置，不出现在最终的属性中
- Mock.random

### 应用
#### web应用
可以在express（or其他能快速构建服务的框架）中集成mockjs，mock后端接口（数据格式定义+mockjs+API实现）

### swagger
见其他博文
### yapi
见其他博文

### Tips
#### .ejs
- 使用时注意：
```
# if mockData里面有 单引号，则会报错，这个时候可以用正则进行替换成转义 ' => \\'
<script>
const mockDataObj = JSON.parse('<%- JSON.stringify(mockData) %>');
</script>
```
- 所以使用时候要注意内容本身，是否会造成错误

## rap2
> 提供给我们统一登录平台的团队，使用的是rap2，可以用来搭建中台的接口平台，文档也可以在里面维护

- 阿里妈妈前端团队出品的开源接口管理工具RAP第二代, rap2.taobao.org
- https://github.com/thx/rap2-delos
- 私有化部署

### 仓库
### 数据字典
- 不同项目的数据表字段
- 字典表（sys_dict）字典表主要存储系统常用的枚举类型数据，主要包含编号、标签、数据值、类型等字段
### 业务身份
- 系统编号｜系统名称｜密钥｜联系人姓名｜联系人邮箱
### 团队
### 接口
### 状态
### 接口标准
- 平台的接口标准
1.appid
appid | appname | appsecret | 业务系统联系人 | 联系人email | 业务系统域名 | 业务系统简介
2.鉴权的规范
对外 && 对内
对外-accesstoken
对内-验签
3.数据包格式
json
通用参数定义-内部服务｜外部服务
状态码定义
返回字段名｜字段类型｜字段说明
status状态编码|msg状态描述|data业务数据
4.服务文档
### 系统通知