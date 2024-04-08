---
title: Flink-overview-summary
date: 2023-01-20 23:25:40
tags:
---
### 项目中对实时计算的需求

- https://github.com/zhisheng17/flink-learning


Apache Flink为应用程序开发提供了以下几种级别的抽象：

1. **Process Functions（处理函数）：** 这是Flink提供的最低级别的抽象。Process Function提供了对每个事件以及注册任意处理时间或事件时间计时器的细粒度控制。这是最灵活，但也最复杂的抽象。

2. **DataStream API（数据流API）：** 这是一个更高级别的抽象，用于处理无界或有界数据。它提供了大量的转换函数，如filter（过滤），map（映射），reduce（减少）等。此API对处理时间窗口和事件时间的处理也有很好的支持，适合需要高级窗口操作的流式处理应用。

3. **Table API 和 SQL：** 这是基于关系模型的声明性API，可以通过SQL查询和Table API进行操作。Table API & SQL 对象模型与数据库表类似，对于经常处理数据分析任务的开发者来讲非常友好，可以获得良好的可读性和多样化的连接器支持。

4. **DataStream-Table Conversion（数据流-表转换）：** DataStream或DataSet也可以被转换成表，进行SQL查询或者Table API操作，再转换回DataStream或DataSet，这种组合使得Flink在处理复杂的、需要混合编程模型的数据流程时也能保持高效和灵活。

在实际开发中，你可以根据具体的使用场景选择适合的抽象级别进行开发。对于复杂的流处理逻辑，可以使用Process Functions，对于标准SQL类的处理，可以选择Table API和SQL。

### flink
Apache Flink目前原生支持Java和Scala，以及通过Table API & SQL 提供对Python的支持。至于Node.js，Apache Flink目前并没有提供对应的原生API支持。

然而，如果你的系统中必须要使用Node.js，你可以通过一些其他的方式来整合。例如，你可以在Node.js应用中利用Flink的REST API进行一些基础的操作，如部署作业，查询作业状态，等等。或者可以使用Kafka等消息中间件作为Flink和Node.js应用之间的桥梁。具体来说，就是Flink从kafka中消费数据，进行处理后，再将结果发送到Kafka，然后Node.js应用再从Kafka中读取这些结果数据。

需要注意的是，这些方法会带来更多的开发和维护工作，你应该根据你的具体需求和实际情况来决定是否需要这样做。