---
title: leetcode-shell-4道题
date: 2021-03-11 13:21:00
tags:
    - leetcode
---

### 192.统计词频
https://leetcode-cn.com/problems/word-frequency/

```
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -r | awk '{print $2, $1}'
```
命令说明：（man cmd）
- cat -- concatenate(link (things) together in a chain or series) and print files
```
(The cat utility reads files sequentially, writing them to the standard output.)
```
- tr -- translate characters
```
(The tr utility copies the standard input to the standard output with sub-stitution or deletion of selected characters.)
(-s      Squeeze multiple occurrences of the characters listed in the last
             operand (either string1 or string2) in the input into a single
             instance of the character.  This occurs after all deletion and
             translation is completed.)
```
- sort -- sort or merge records (lines) of text and binary files
```
-r, --reverse
             Sort in reverse order.
```
- uniq -- report or filter out repeated lines in a file
```
-c      Precede each output line with the count of the number of times
             the line occurred in the input, followed by a single space.
```
- awk - pattern-directed scanning and processing language（很强大，只用他也能完成这个任务，不过如果是只用这个的话，也可以用编写起来更趁手的python或者node来处理了）

分词这一步```tr -s ' ' '\n'```也可以替换成```xargs -n1```

### 193.有效电话号码
https://leetcode-cn.com/problems/valid-phone-numbers/

- 分析正则
- 使用grep/awk/gawk都可