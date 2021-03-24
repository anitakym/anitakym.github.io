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