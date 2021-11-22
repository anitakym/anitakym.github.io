---
title: unicode综述
date: 2021-11-10 15:59:58
tags:
---
### 涉及unicode的博文
- dart-sass
- iconfont使用经验总结
- https://dmitripavlutin.com/what-every-javascript-developer-should-know-about-unicode/#comments
```
Table of Contents
1. The idea behind Unicode
2. Basic Unicode terms
2.1 Characters and code points
2.2 Unicode planes
2.3 Code units
2.4 Surrogate pairs
2.5 Combining marks
3. Unicode in JavaScript
3.1 Escape sequences
3.2 String comparison
3.3 String length
3.4 Character positioning
3.5 Regular expression match
4. Summary
```
- 上面这篇讲解很详尽
### 零宽字符
- Unicode 中还有一类格式字符，不可见，不可打印，主要作用于调整字符的显示格式，所以我们将其称为零宽字符。
```
零宽字符主要有以下几类：

零宽度空格符 (zero-width space) U+200B : 用于较长单词的换行分隔。

零宽度非断空格符 (zero width no-break space) U+FEFF : 用于阻止特定位置的换行分隔。

零宽度连字符 (zero-width joiner) U+200D : 用于阿拉伯文与印度语系等文字中，使不会发生连字的字符间产生连字效果。

零宽度断字符 (zero-width non-joiner) U+200C : 用于阿拉伯文、德文、印度语系等文字中，阻止会发生连字的字符间的连字效果。

左至右符 (left-to-right mark) U+200E : 用于在混合文字方向的多种语言文本中（例：混合左至右书写的英语与右至左书写的希伯来语），规定排版文字书写方向为左至右。

右至左符 (right-to-left mark) U+200F : 用于在混合文字方向的多种语言文本中，规定排版文字书写方向为右至左
```
- 可用来做隐形水印
- 对于用户录入内容中的零宽字符，注意处理；