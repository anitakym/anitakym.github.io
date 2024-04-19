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



### other cases
#### A
hystrix - https://github.com/Netflix/Hystrix
```
Hystrix是一个用于分布式系统的容错库，它主要用于隔离访问远程系统、服务和第三方库的节点，防止其故障级联到其它部分影响整个系统。
Hystrix通过提供线程池、超时设置、熔断器（Circuit Breaker）以及监控和实时配置等一系列工具，给微服务带来了稳定性和弹性。 
Hystrix是Netflix开源项目的一部分，用Java编写，并且基于Java的并发和异步库实现。

使用Hystrix的主要优点如下：

1. 提供熔断器：通过使用熔断器模式来防止对不稳定服务的访问。当服务连续发生一定数量的错误时，熔断器会“熔断”，此时会快速返回一个默认结果而不是继续访问故障服务。当故障服务回复后，熔断器会自动“闭合”，重新允许对服务的访问。

2. 线程隔离： Hystrix使用线程池来隔离对远程服务的访问，这样您可以控制使用的并发，防止一个服务的崩溃导致整个系统崩溃。

3. 超时设置：你可以为每个远程服务调用设置超时时间，以便在服务未在规定时间内响应时终止访问。

4. 提供指标和监控：Hystrix提供了实时监控指标，以便你可以跟踪每个服务的性能，包括成功、失败、熔断和线程使用的统计数据。

5. 使用Fallback：当远程服务调用错误或超时时，Hystrix提供了fallback方法，允许你返回指定的默认值，确保微服务在故障的情况下依然可以返回有用的信息。

总之，Hystrix可提高分布式系统的稳定性、弹性和容错能力。 在网络和服务不稳定的情况下，Hystrix能起到很大作用。
```
降级方案 - 系统之间feign调用

#### B
- sentinel - 资源|规则 - 流量控制-自由选择控制的角度，灵活组合，从而达到想要的效果 -熔断降级-降低调用链路中的不稳定资源 - 系统负载保护
- sentinel(面向分布式服务架构的流量控制组件) - 适配feign
```
feign.sentinel.enable=true
error
NoSuchMethodErrorfeign.RequestTemplate.path（）Ljava / lang / String;
版本不匹配 - spring-cloud-starter-alibaba-sentinel feign-core
解决 - 添加流量规则
Method：http://service-name/path
```
https://sentinelguard.io/zh-cn/docs/introduction.html
```
Sentinel 介绍
随着微服务的流行，服务和服务之间的稳定性变得越来越重要。Sentinel 是面向分布式、多语言异构化服务架构的流量治理组件，主要以流量为切入点，从流量路由、流量控制、流量整形、熔断降级、系统自适应过载保护、热点流量防护等多个维度来帮助开发者保障微服务的稳定性。

Sentinel 的历史
2012 年，Sentinel 诞生，主要功能为入口流量控制。
2013-2017 年，Sentinel 在阿里巴巴集团内部迅速发展，成为基础技术模块，覆盖了所有的核心场景。Sentinel 也因此积累了大量的流量归整场景以及生产实践。
2018 年，Sentinel 开源，并持续演进。
2019 年，Sentinel 朝着多语言扩展的方向不断探索，推出 C++ 原生版本，同时针对 Service Mesh 场景也推出了 Envoy 集群流量控制支持，以解决 Service Mesh 架构下多语言限流的问题。
2020 年，推出 Sentinel Go 版本，继续朝着云原生方向演进。
2021 年，Sentinel 正在朝着 2.0 云原生高可用决策中心组件进行演进；同时推出了 Sentinel Rust 原生版本。同时我们也在 Rust 社区进行了 Envoy WASM extension 及 eBPF extension 等场景探索。
2022 年，Sentinel 品牌升级为流量治理，领域涵盖流量路由/调度、流量染色、流控降级、过载保护/实例摘除等；同时社区将流量治理相关标准抽出到 OpenSergo 标准中，Sentinel 作为流量治理标准实现。
```
https://opensergo.io/zh-cn/
微服务治理

#### C
okhttp3性能 > httpclient
feign底层 更换为 okhttp3
