---
title: sed
date: 2023-01-21 00:01:12
tags:
---
> 之前写过一个awk,见之前博文2020-03-12的awk

`sed`（stream editor）是一个在 Unix、Linux 和 macOS 上常用的命令行文本处理工具，它用于对文本文件的内容执行基本的文本转换。操作形式包括：插入、删除、追加、查找和替换。`sed` 常用于脚本和管道处理中。

常用的 `sed` 命令格式如下：

```
sed [options] 'script' input_file
```

1. options: 选项，可选。
2. script: 脚本，为 `sed` 命令
3. input_file: 输入文件，作用的文本文件。

以下是一些常用的 `sed` 选项：

- `-e`: 允许在同一个文件中执行多个编辑操作
- `-i`: 对文件执行原地编辑，即将操作后的内容覆盖到源文件
- `-n`: 操作后的内容只输出到终端，源文件不受影响

以下是一些常用的 `sed` 命令：

1. 替换文本中的字符串（要注意转义符）：

```
sed 's/old-string/new-string/g' input_file
```

上述命令会将 `input_file` 中所有的 `old-string` 字符串替换为 `new-string`。


2. 删除文本中的某行：

```
sed 'nd' input_file
```

其中，`n` 表示行号，例如 `3d` 则表示删除第三行。

3. 添加新行（在某行之前或之后）：

在第 `n` 行之前添加新行：

```
sed 'nia\\
new_line_content' input_file
```

在第 `n` 行之后添加新行：

```
sed 'na\\
new_line_content' input_file
```

请注意 a 和 i 的位置：'a' 表示在该行之后添加，'i' 表示在该行之前添加。

这些仅是 `sed` 的一些基本操作。`sed` 还可以执行复杂的文本编辑和过滤操作，例如正则表达式匹配。
