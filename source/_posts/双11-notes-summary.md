---
title: 双11-notes-summary
date: 2021-11-03 15:35:33
tags:
---
> 又到双11了，发现每年ali都会出双11技术总结的手册，看了下，记个summary

## Concepts

### Words
#### CVR - Conversion rate, term used to calculate website visitors in Internet marketing
#### CTR - Click-Through Rate 

## Details
### 支付宝
- 金融 - 分布式 - 一致性
- 云计算 - 云服务
- 容器 - 离线服务器资源临时用于在线业务
- OceanBase - 三地五中心
- GeaBase - 风控
- 客服 - 查询应答 快捷应答 未问先答（AI训练）
- 可靠性，安全性

### 苏宁API
#### 异常码
- 唯一性，风格一致，有层级有分类，可扩展
- 分类 - 系统级 ｜ 业务级
- 系统级 - 流控 ｜ 权限 ｜ 系统校验 ｜ 服务不可用
- 业务级 - 业务字段（非空｜格式｜枚举）｜业务场景（单场景｜组合场景）
- 解决的问题 - 异常码监控 ｜ 接口告警 ｜ 定位及快速解决问题