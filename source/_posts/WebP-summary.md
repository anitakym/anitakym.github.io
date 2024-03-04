---
title: WebP-summary
date: 2024-03-04 10:15:44
tags:
---
### caniuse
- https://caniuse.com/?search=webp
- WebP image format  - OTHER
Image format (based on the VP8 video format) that supports lossy and lossless compression, as well as animation and alpha transparency. WebP generally has better compression than JPEG, PNG and GIF and is designed to supersede them. AVIF and JPEG XL are designed to supersede WebP.
- Safari 14.0 – 15.6 has full support of WebP, but requires macOS 11 Big Sur or later.

### Picture
- caniuse ok ~
- https://cloud.tencent.com/document/product/436/60453
- 可配合资源的文档对象存储和数据万象处理

### 兼容性
- 尤其是在涉及canvas的时候，要注意Safari上面的兼容性

### 成本考虑
- 结合使用场景
- https://cloud.tencent.com/document/product/460/58117

### COS数据处理接口
- 下载｜上传｜云上数据
- 图片压缩指在图片质量保持不变的情况，尽可能的减小图片大小，以达到节省图片存储空间、减少图片访问流量、提升图片访问速度的效果。
对象存储（Cloud Object Storage，COS）基于 数据万象（Cloud Infinite，CI） 产品推出了 WebP 压缩功能，可将图片转换为 webp 压缩图片格式，其在压缩方面相比 jpg 格式更优越。在相同图片质量的情况下，webp 格式图片要比 jpg 格式图片减小25%以上，可以适配多终端使用场景。
- http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp