---
title: bonree-项目经验-summary
date: 2023-01-20 23:27:08
tags:
---
- https://www.bonree.com/

- 公司采购的，android和IOS端都接入了，作为问题上报，排查监控的工具


#### 网络问题
- 发现切换到特定网络后，报网络问题，ip已解析出来没问题，但是客户端的连通性有问题
- https://cloud.tencent.com/document/product/213/14638
- 帮忙收集下mtr的信息，我们看看具体是哪个设备的问题，目前看目的端是正常。初步看应该是在客户端或者中间设备有异常
- 如果用户是手机端的话，可以安装这个工具来探测：IOS：iNetTools 到App Store安装下，免费的 安卓：pingTools，到应用商店安装下，免费
