---
title: PAI-DSW
date: 2021-08-30 10:57:37
tags:
---

> 阿里云的 DSW（PAI-DSW（Data Science Workshop）是 PAI 推出的在线深度学习开发平台）

### 文档指路

https://help.aliyun.com/document_detail/102789.html#section-o64-ypv-8ow

```
本文为您介绍PAI-DSW的相关问题。

什么是PAI-DSW？
PAI-DSW实例如何挂载和使用自己的NAS文件系统？
如何在PAI-DSW中使用第三方库
运行机器学习代码时，为什么页面放置一段时间后提示重新登录？
使用ECS搭建FTP上传下载文件到NAS，执行挂载（mount）命令报错mount:wrong fs type,bad option,bad superlock
如何使用PAI-DSW读取OSS数据？
为什么安装的第三方包没有生效？
如何部署PAI-DSW生成的模型？
PAI-DSW如何收费？
如何查看PAI-DSW账单？
```

目录如上

### NAS 挂载问题

#### 阿里云文档

```

PAI-DSW实例如何挂载和使用自己的NAS文件系统？
PAI-DSW实例默认提供的系统盘为临时存储，在停止或删除实例后，系统会清空数据。如果您需要永久化存储数据，则需要挂载自己NAS。您所有的NAS文件均存储在/nas目录，可以通过PAI-DSW Terminal进入该目录查看并使用文件。

新版的PAI-DSW仅支持在创建实例时，挂载自己的NAS，详情请参见创建实例。实例一旦创建，则无法编辑实例信息或挂载NAS。
```

#### 具体操作

对 ECS 实例进行配置&&挂载 NFS

```
# 安装NFS客户端
sudo apt-get update
sudo apt-get install nfs-common

# 修改NFS请求数量限制
sudo echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
sudo echo "options sunrpc tcp_max_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf

# 执行挂载NFS的命令
sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 挂载点地址

# 验证是否挂载成功
df -h | grep aliyun
```
