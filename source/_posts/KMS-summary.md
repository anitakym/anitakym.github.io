---
title: KMS-summary
date: 2024-03-22 13:48:56
tags:
---
KMS（Key Management Service）是云计算服务商提供的密钥管理服务。它主要针对数据加密、签名、身份认证等场景，提供自主控制和管理密钥的能力。

KMS提供了一种在不暴露密钥明文的情况下，使用密钥完成客户数据的加密和解密操作。用户可以放心将密钥托管在KMS，不必担心密钥的安全。

使用KMS进行数据加密的流程一般如下：

1. 用户使用KMS创建一个密钥或者使用现有的密钥。

2. 用户将需要加密的数据提交给KMS，并指定使用的密钥。

3. KMS使用指定的密钥进行加密操作，并返回加密后的数据。

4. 加密后的数据可以安全地存储在任意位置。只有拥有密钥权限的用户才能通过KMS进行解密。

5. 用户需要解密数据时，将加密后的数据提交给KMS，并指定解密的密钥。

6. KMS使用密钥进行解密操作，并返回原始数据。

KMS的好处是，用户无需担心密钥的生成、存储、使用和管理等复杂的问题。只需专注于业务开发，将安全问题交给KMS处理。同时，KMS还有严格的权限控制和审计日志功能，可以追踪和记录所有密钥操作，协助满足合规需求。

- https://cloud.tencent.com/document/product/457/45594


### aes加密CBC模式，paddingzero填充
AES（Advanced Encryption Standard，高级加密标准）是一种对称加密算法，是目前最常用的加密方式之一。CBC（Cipher Block Chaining，密码块链）是分组密码的一种工作模式，每个明文块先与前一个密文块进行异或后，再进行加密。

在模式中，可能会遇到明文长度不是密钥长度的整数倍的情况，这就需要一个填充（padding）步骤。

在Padding Zero模式下，你会在明文的后面添加0，直到明文的长度到达密钥长度的整数倍。例如，假设块大小为64位，而消息只有40位，那么就在后面添加24位的0。

然而，PaddingZero有一个问题，那就是当数据拥有真正的0值时，这个方案可能会引起混淆。为了解决这个问题，就出现了PKCS7等其他填充方式，但具体用哪个方式取决于你的具体需求和环境。

一个完整的AES CBC加密流程，包括了这样几个步骤：
1. 对明文进行必要的填充。
2. 初始向量IV的选择。
3. 按照CBC模式，进行分块异或和加密操作。
4. 输出密文。

nodejs (crypto)