---
title: auth相关
date: 2023-03-23 20:13:42
tags:
---
APP_TOKEN_CACHE_KEY 是一个常量值，通常在开发移动应用时使用。它表示在客户端（如 Android 或 iOS 应用）中缓存应用程序的访问令牌（Access Token）所使用的键名。

Access Token 是一种用于授权访问受保护资源的凭证，通常在 OAuth 2.0 认证流程中使用。为了避免频繁地从授权服务器（如 Auth0、Okta 等）请求新的 Access Token，我们通常会在客户端中将其缓存起来，并在需要时直接使用缓存中的值

## OAuth
- 2007 年 OAuth 1.0 面世
- 2011 OAuth 2.0 草案


#### reference
- OAuth2协议规范
- OpenID Connect explained

#### Lucia
- https://github.com/lucia-auth/lucia


### 微信登录
- code只有一次有效。无论调用成功与否，只要发起httprequest，这个code就被消费掉了。需要重新获取code。
- 是的，微信官方的登录凭证（code）是唯一的，每次用户在微信登录后服务器都会返回一个新的code。这是为了保证每次用户操作的安全性和唯一性。所以理论上来说，每一个code只能使用一次，使用后就会失效。

这正体现了幂等性的原理，即不论操作执行一次还是多次，效果都是一样的。也就是说，无论一个code使用多少次，结果都是一致的，这个结果就是该code失效。

这样既保证了用户信息的安全，也提高了系统的效率，因为系统只需要处理一次操作，而不是处理多次相同的操作。