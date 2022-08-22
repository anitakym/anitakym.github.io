---
title: 微信网页开发-summary
date: 2022-04-28 14:53:26
tags:
---
> 2015年初，微信发布了一整套网页开发工具包，称之为 JS-SDK，开放了拍摄、录音、语音识别、二维码、地图、支付、分享、卡券等几十个API.​JS-SDK是对之前的 WeixinJSBridge 的一个包装，以及新能力的释放，并且由对内开放转为了对所有开发者开放

- https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/#%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%8A%80%E6%9C%AF%E5%8F%91%E5%B1%95%E5%8F%B2
- 上面是 - 小程序技术发展史

- https://fjc0k.github.io/vtils/

- https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_Open_Tag.html#21
- https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/url-scheme/urlscheme.generate.html

#### webview ua
- 和微信内打开网页一样，ua情况
- https://developers.weixin.qq.com/doc/offiaccount/WiFi_via_WeChat/WiFi_Hardware_Authentication_Protocol_Interface_Description.html
```
2. 如何识别 http 请求是否来自微信客户端
在 http 数据包的 header 结构中解析“User-Agent”即可，判断是否包含关键字“micromessenger”（这里请注意不要拦截其他微信 http 请求，所以关键词请匹配好），示例代码如下：
String userAgent = request.getHeader("User-Agent");
if(userAgent.matches(".*micromessenger.*")){  response.sendRedirect("http://www.foo.com/portal/portal.html?authUrl=http%3A%2F%2Fwww.foo.com%2Fportal%2Fauth.html&extend=xxx ");			
}
```
微信客户端将解析Portal Server转跳地址中的 authUrl 和extend参数，继续完成连接流程。
但是的确有用户反馈微信打开之后，没有对应微信跟进ua进行的提示，查了下pv日志，对应用户使用的是钉钉环境，待跟进这个

#### 扫码或者分享的链接打开，触发SDK
