---
title: auth相关
date: 2023-03-23 20:13:42
tags:
---
APP_TOKEN_CACHE_KEY 是一个常量值，通常在开发移动应用时使用。它表示在客户端（如 Android 或 iOS 应用）中缓存应用程序的访问令牌（Access Token）所使用的键名。

Access Token 是一种用于授权访问受保护资源的凭证，通常在 OAuth 2.0 认证流程中使用。为了避免频繁地从授权服务器（如 Auth0、Okta 等）请求新的 Access Token，我们通常会在客户端中将其缓存起来，并在需要时直接使用缓存中的值