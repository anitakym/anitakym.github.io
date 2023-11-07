---
title: protobuf
date: 2018-10-16 17:15:10
tags:
---
## 文档指南
- https://developers.google.com/protocol-buffers
- github: https://github.com/protocolbuffers/protobuf

## 说明
- Google Protocol Buffer
- 数据序列化协议
- 压缩和传输效率极高，语法也简单
- 是独立的协议系统，所以它和开发语言、运行平台都没有关系，可以用在扩展的序列化结构数据格式。目前提供了 C++、Java、Python 、Ruby、Go 等语言的开发接口 API
- protobuf使用的是二进制格式，因此，每种语言都需要有个生成器。
- 使用protobuf时，需要事先在proto文件中声明结构每一个需要序列化和反序列化数据的服务都需要添加相应的proto文件，然后使用生成器生成一个包含数据的对象
- Protobuf 对于 1M 以下的 message 有很高的效率，但是当 message 大于 1M 的时候，Protobuf 的效率会逐步降低


## 应用
- 用于 RPC 系统和持续数据存储系统
- gRPC 把 Protobuf 作为底层的编解码协议
- gRPC也使用了协议缓冲区（也称为protobuf），它提供了一种将结构化数据定义和序列化为高效的二进制格式的方法。由于它们是二进制格式的，所以它们的传输量相对更小，可以快速在线上传输。
- 对于性能要求高并且数据量大的应用而言，protobuf常常是最佳的选择

### protobuf.js
用的时候，不要用protobuf.min.js

reads output from proto2json as a schema
encodes objects to buffers
decodes buffers to objects