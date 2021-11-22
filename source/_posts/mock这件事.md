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