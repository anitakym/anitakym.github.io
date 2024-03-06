---
title: node-ReadableStream
date: 2021-06-22 11:03:47
tags:
---

### readablestream
- 在 JavaScript 中, Streams API 的 ReadableStream 允许你在一段长时间内读取一段数据而不是一次性获取所有数据。这对于处理网络响应、文件读写等提供了极大的便利，特别是在处理大文件或者实时数据时，我们可以边读边处理，提高性能并提升用户体验。

ReadableStream 非常适合配合 `for await...of` 循环进行异步迭代。以下面这个从网络获取文本的例子来说明：

```javascript
async function logChunks(readableStream) {
  const reader = readableStream.getReader();
  try {
    for await (const chunk of reader) {
      console.log(chunk);
    }
  } finally {
    reader.releaseLock();
  }
}

fetch('https://some.url/')
.then((response) => logChunks(response.body));
```

在这个示例中，我们创建了一个 `ReadableStream` 的 reader，并在 `for await...of` 中异步迭代这个 reader。每个 chunk 是 `ReadableStream` 中的一部分数据。我们打印出每个 chunk，直到我们处理完所有的数据。

注意，一旦我们处理完所有数据，或者发生错误，我们需要调用 `reader.releaseLock()` 来释放对 `ReadableStream` 的锁定，以便后续的代码可以继续使用这个 `ReadableStream`。

上述例子中的 `for await...of` 会等待每次迭代的 promises 完成，所以我们会按照流中数据的顺序来处理数据。如果因为某种原因我们需要停止读取流，我们可以简单地 `break` 掉 `for await...of` 循环，这将会释放流的锁定。

#### web
- https://chromestatus.com/feature/5143121161879552?context=myfeatures

### diff
在 Node.js 和浏览器环境中，ReadableStream 的异步迭代处理会有些差异。

1. 浏览器环境：

在浏览器环境中，你可以直接利用 Streams API 的 ReadableStream 进行异步迭代。这是因为 Streams API 是 Web 平台的一部分，所以在浏览器原生支持。

例如，当你从网络获取数据时，你可以如下操作：
```javascript
async function processData(readableStream) {
    const reader = readableStream.getReader();
    try {
        for await (const chunk of reader.read()) {
            console.log(chunk);
        }
    } catch(err){
        console.error("Error:", err);
    } finally {
        reader.releaseLock();
    }
}

fetch('https://example.com/')
     .then(response => processData(response.body))
     .catch(err => console.error(err));
```
这种方式的优势在于，你可以立即开始处理数据，而不必等到所有数据下载完成。

2. Node.js 环境：

Node.js 利用的是 Stream 模块，它与浏览器中的 Streams API 略有不同，但是设计的初衷是类似的。Node.js 中的 readable stream 也支持异步迭代。

例如，如果你正在从文件中读取数据，你可以这样操作：

```javascript
const fs = require('fs');
async function readStream() {
  const readableStream = fs.createReadStream('example.txt', { encoding: 'utf8', highWaterMark: 1024 });
  for await (const chunk of readableStream) {
    console.log(chunk);
  }
}
readStream();
```
在这个示例中，我们使用 `fs.createReadStream` 创建了一个 readable stream，然后使用异步迭代进行读取。