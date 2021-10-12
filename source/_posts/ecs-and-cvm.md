---
title: ecs-and-cvm
date: 2021-10-06 13:52:27
tags:
---
> 17年到现在，团队在阿里云和腾讯云之间切换了几回（各种原因），现对于使用过的产品做下梳理；

# 阿里云

## 网络与CDN - 负载均衡
### 文档
- https://help.aliyun.com/document_detail/196874.html
- 

### TIPS
- 计费 ｜ 可用区（单｜多）

## 云服务器 - ECS
### 文档

### Basic
- Elastic Compute Service
- 基于虚拟化资源池
- 多线BGP
  - border gateway protocol 边界网关协议 - 配置在路由上
  - 三网（跨运营商）
  - 解决不同网络之间的差异
  - 动态｜静态BGP - https://developer.aliyun.com/article/179417
- 专线

#### 创建
- 地域 - 可用区
- “不同地域的实例之间内网互不相通；选择靠近您客户的地域，可降低网络时延、提高您客户的访问速度”
- 用户所在地 
- 相关别的产品也买在相同可用区
- 数据备份，冗余，异地多活


## 控制台Tips
- APP｜Web
- Web全功能，也在不断改进体验 - console域下
- 善用站点提供的搜索功能
- 公司账号 - 费用和工单 - 按量计费｜包年包月
- 腾讯云我们是比较大的用户，会有专门的客服QQ群，回复还是非常及时的（不同支持时效收费也不一样，和每年消费的额度到达某个额度也相关，各部分服务的折扣也和消费额度相关）

# 腾讯云

### NAT
- https://cloud.tencent.com/document/product/552/12951
# 其他

## Tengine
- 配置nginx的时候走这个
- http://tengine.taobao.org/

