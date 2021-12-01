---
title: 升https
date: 2020-08-11 16:59:53
tags:
  - SSL
  - HTTP
---

* 名词解释

#### SSL
SSL (Secure Sockets Layer) and its successor, TLS (Transport Layer Security), are protocols for establishing authenticated and encrypted links between networked computers. Although the SSL protocol was deprecated with the release of TLS 1.0 in 1999, it is still common to refer to these related technologies as “SSL” or “SSL/TLS.” The most current version is TLS 1.3, defined in RFC 8446(https://tools.ietf.org/html/rfc8446) (August 2018).
- 为互联网通信提供安全及数据完整性保障
- SSL证书是CA对用户公钥的认证

#### CA
A certificate authority (CA), also sometimes referred to as a certification authority, is a company or organization that acts to validate the identities of entities (such as websites, email addresses, companies, or individual persons) and bind them to cryptographic keys through the issuance of electronic documents known as digital certificates. A digital certificate provides:
CA机构，是承担公钥合法性检验的第三方权威机构，负责指定政策、步骤来验证用户的身份，并对SSL证书进行签名，确保证书持有者的身份和公钥的所有权。

- Authentication, by serving as a credential to validate the identity of the entity that it is issued to.
- Encryption, for secure communication over insecure networks such as the Internet.
- Integrity of documents signed with the certificate so that they cannot be altered by a third party in transit.


![](ca-diagram-b.png)

cite(https://www.ssl.com/faqs/what-is-a-certificate-authority/)
