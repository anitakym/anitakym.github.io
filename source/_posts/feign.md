---
title: feign
date: 2021-03-15 11:35:27
tags:
---
#### 最近要接入神策埋点，数据采集接入的话，API接入部分，使用feign api方式调用

```
How does Feign work?
Feign works by processing annotations into a templatized request. Arguments are applied to these templates in a straightforward fashion before output. Although Feign is limited to supporting text-based APIs, it dramatically simplifies system aspects such as replaying requests. Furthermore, Feign makes it easy to unit test your conversions knowing this.
```
#### 文档指南：
https://github.com/OpenFeign/feign

为什么要使用feign呢？





#### feign的扩展：

提高扩展性，使用者可以不修改框架源码的情况下，为框架扩展新的功能（类似于插件模式）
feign 是一个 HTTP 客户端框架，我们可以在不修改框架源码的情况下，用如下方式来扩展我们自己的编解码方式、日志、拦截器等。
```

Feign feign = Feign.builder()
        .logger(new CustomizedLogger())
        .encoder(new FormEncoder(new JacksonEncoder()))
        .decoder(new JacksonDecoder())
        .errorDecoder(new ResponseErrorDecoder())
        .requestInterceptor(new RequestHeadersInterceptor()).build();

public class RequestHeadersInterceptor implements RequestInterceptor {  
  @Override
  public void apply(RequestTemplate template) {
    template.header("appId", "...");
    template.header("version", "...");
    template.header("timestamp", "...");
    template.header("token", "...");
    template.header("idempotent-token", "...");
    template.header("sequence-id", "...");
}

public class CustomizedLogger extends feign.Logger {
  //...
}

public class ResponseErrorDecoder implements ErrorDecoder {
  @Override
  public Exception decode(String methodKey, Response response) {
    //...
  }
}
```