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

### protocol-relative url的问题
- https://www.paulirish.com/2010/the-protocol-relative-url/
- 尽量避免使用
```
Update 2014.12.17:

Now that SSL is encouraged for everyone and doesn’t have performance concerns, this technique is now an anti-pattern. If the asset you need is available on SSL, then always use the https:// asset.

Allowing the snippet to request over HTTP opens the door for attacks like the recent Github Man-on-the-side attack. It’s always safe to request HTTPS assets even if your site is on HTTP, however the reverse is not true.

More guidance and details in Eric Mills’ guide to CDNs & HTTPS and digitalgov.gov’s writeup on secure analytics hosting.
```

### cases
```
curl https://xxxx.xxx.cn
curl: (60) SSL: no alternative certificate subject name matches target host name 'xxxx.xxx.cn'
More details here: https://curl.haxx.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```
进入Chrome看，可以点击小锁，看具体的证书信息

### SSL证书生成
- 17年开始，如果不是https,chrome会被标记不安全 苹果要求都是https；不用https，很容易被运营商劫持
- 证书的安全级别 证书的更新
- 七牛云（一年1900） 阿里云 腾讯云
- 拿到证书，scp上传到服务器上
```
mv ssl /www/
/nginx/conf.d server部分配置ssl
# 运维，安全
help.aliyun.com
```

### https | http
#### ajax-using-https-on-an-http-page
- https://stackoverflow.com/questions/1105934/ajax-using-https-on-an-http-page
#### how-can-i-make-an-http-request-from-an-https-website
- https://stackoverflow.com/questions/53211319/how-can-i-make-an-http-request-from-an-https-website


#### cookies set不了的问题
- https://stackoverflow.com/questions/62578201/how-to-fix-this-set-cookie-was-blocked-due-to-user-preferences-in-chrome-sta
- https://angel.co/today/stories/chrome-83-arrives-with-redesigned-security-settings-third-party-cookies-blocked-in-incognito-21796
