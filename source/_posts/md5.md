---
title: md5
date: 2021-03-24 14:05:24
tags:
---

### 库
[crypto-js](https://www.npmjs.com/package/crypto-js)
[object-hash](https://www.npmjs.com/package/object-hash)
[node-forge](https://github.com/digitalbazaar/forge)
[spark-md5](https://www.npmjs.com/package/spark-md5)

### SparkMD5
- SparkMD5是MD5算法的一个快速MD5实现。这个脚本是基于JKM md5库的，它是最快的算法。这是最适合浏览器使用的，因为nodejs版本可能更快。

#### 对JKM md5库的改进。
- 字符串被转换为utf8，就像大多数服务器端算法一样。
- 修正大量数据的计算(溢出)
- 增量式md5（见下文）。
- 支持数组缓冲区（类型化数组）。
- 功能被封装在closure(闭包)中，以避免全局赋值。
- 面向对象的库
- CommonJS(它可以在node中使用)和AMD集成
- 通过JSHint和JSCS校验

增量式md5对于大量数据的哈希处理，例如文件，表现得更好。我们可以使用FileReader和Blob来分块读取文件，并在保持低内存使用率的情况下，追加每个分块进行md5哈希。


### 代码调试
本身包很小22K，代码也比较清楚

开发工具是vscode
```
// Type definitions for spark-md5 3.0
// Project: https://github.com/satazor/js-spark-md5#readme
// Definitions by: Bastien Moulia <https://github.com/bastienmoulia>
//                 Florian Keller <https://github.com/ffflorian>
// Definitions: https://github.com/DefinitelyTyped/DefinitelyTyped
// TypeScript Version: 2.3

// copy of ArrayBuffer because of a conflict with the class SparkMD5.ArrayBuffer
type JsArrayBuffer = ArrayBuffer;

declare class SparkMD5 {
    constructor();

    static hash(str: string, raw?: boolean): string;
    static hashBinary(content: string, raw?: boolean): string;

    append(str: string): SparkMD5;
    appendBinary(contents: string): SparkMD5;
    destroy(): void;
    end(raw?: boolean): string;
    getState(): SparkMD5.State;
    reset(): SparkMD5;
    setState(state: SparkMD5.State): SparkMD5.State;
}

declare namespace SparkMD5 {
    interface State {
        buff: Uint8Array;
        hash: number[];
        length: number;
    }

    class ArrayBuffer {
        constructor();

        static hash(arr: JsArrayBuffer, raw?: boolean): string;

        append(str: JsArrayBuffer): ArrayBuffer;
        destroy(): void;
        end(raw?: boolean): string;
        getState(): State;
        reset(): ArrayBuffer;
        setState(state: State): State;
    }
}

export = SparkMD5;
```
Library/Caches/typescript/4.2/node_modules/@types/spark-md5/index.d.ts
因为vscode默认开启了AutomaticTypeAcquisition

https://code.visualstudio.com/Docs/languages/javascript#_automatic-type-acquisition

如果想要关闭的话，可以设置里面 disableAutomaticTypeAcquisition

这样我们可以看到类型定义，本身node_modules里面 spark-md5是没有类型声明的


### 实例调试
我们应用场景是对视频做checkmd5,每秒钟50M的样子～

### 读取文件
https://github.com/forsigner/browser-md5-file/blob/master/src/index.js
```
import SparkMD5 from 'spark-md5'

export default class BMF {
  md5(file, md5Fn, progressFn) {
    this.aborted = false
    this.progress = 0
    let currentChunk = 0
    const blobSlice =
      File.prototype.slice ||
      File.prototype.mozSlice ||
      File.prototype.webkitSlice
    const chunkSize = 2097152
    const chunks = Math.ceil(file.size / chunkSize)
    const spark = new SparkMD5.ArrayBuffer()
    const reader = new FileReader()

    loadNext()

    reader.onloadend = e => {
      spark.append(e.target.result) // Append array buffer
      currentChunk++
      this.progress = currentChunk / chunks

      if (progressFn && typeof progressFn === 'function') {
        progressFn(this.progress)
      }

      if (this.aborted) {
        md5Fn('aborted')
        return
      }

      if (currentChunk < chunks) {
        loadNext()
      } else {
        md5Fn(null, spark.end())
      }
    }

    function loadNext() {
      const start = currentChunk * chunkSize
      const end = start + chunkSize >= file.size ? file.size : start + chunkSize
      reader.readAsArrayBuffer(blobSlice.call(file, start, end))
    }
  }

  abort() {
    this.aborted = true
  }
}

```
- FileReader(https://developer.mozilla.org/en-US/docs/Web/API/FileReader)
最好直接看英文的，中文的翻译有点问题，而且内容更新不及时！！！
<pre>
FileReader can only access the contents of files that the user has explicitly selected, either using an HTML <input type="file"> element or by drag and drop. It cannot be used to read a file by pathname from the user's file system. To read files on the client's file system by pathname, use the File System Access API. To read server-side files, use standard Ajax solutions, with CORS permission if reading cross-domain.
</pre>
<pre>
FileReader 对象允许 Web 应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 File 或 Blob 对象来指定要读取的文件或数据。

文件对象可以从用户使用 <input> 元素选择文件后返回的 FileList 对象中获取，也可以从拖放操作的 DataTransfer 对象中获取，或者从 HTMLCanvasElement 上的 mozGetAsFile() API 中获取。

FileReader 只能使用 HTML <input type="file"> 元素或通过拖放来访问用户已明确选择的文件内容。它不能用于从用户的文件系统中按路径名读取文件。要通过路径名读取客户端文件系统中的文件，请使用文件系统访问API。要读取服务器端文件，请使用标准的Ajax解决方案，如果跨域读取，请使用CORS权限。
</pre>

- https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsDataURL