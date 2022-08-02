---
title: XSS
date: 2022-07-14 09:38:22
tags:
---
## baiscs
- Cross_Site_Scripting
- 


- 安全组建议 - 整站过滤
```
一些cases：
- 过滤"<"、">"将用户输入放入引号间，基本实现数据与代码隔离
- 过滤单引号和双引号防止用户跨越许可的标记，添加自定义标记
- 过滤TAB和空格,防止关键字被拆分
- 过滤script等关键字
- 过滤&#,防止HTML属性绕过检查
```
- https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html#introduction

### Vue
- https://vuejs.org/guide/best-practices/security.html (里面有各种情况，及best practices)
- https://github.com/LeSuisse/vue-dompurify-html
- https://www.npmjs.com/package/xss
- 以上，可以配合使用，核心规则是 - 不要用v-html 渲染不可信的内容
```
Rule No.1: Never Use Non-trusted Templates#
The most fundamental security rule when using Vue is never use non-trusted content as your component template.
```

### 渗透测试
- OWASP ZAP
- 