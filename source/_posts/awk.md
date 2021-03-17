---
title: awk
date: 2020-03-02 11:42:56
tags:
    - 工具篇
---
> 上服务器查一些简单的日志，整理一些需要的数据，用到awk
> man awk => 用法指南(pattern-directed scanning and processing language)
> 能够直接支持正则表达式(grep和sed也是)

### 历史
1979年，在unix系统上出现了一个名为AWK的宏与文本处理语言，被普遍认为是一种脚本语言；
创建者命名为：样式扫描和处理语言
AWK主要用于处理文本，也是现在正则表达式的前身
AWK的设计思想收到SNOBOL的影响
### 闲聊
- vim和sed,awk的区别
vim是交互式的，文件操作模式
sed,awk是非交互式的，行操作模式

- sed一般用于对文本内容做替换
```
sed 's/要被取代的字串/新的字串/g'
```

- awk一般用于对文本内容进行统计，按照需要的格式进行输出

- awk更像是脚本语言，用于相对比较规范的文本处理，统计数量并输出指定字段，sed用于将不规范的文本，处理成比较规范的文本

### 使用场景
```
ps -ef | grep 关键字 | awk '{print $2}' | xargs kill -9
```

```
# 分析日志
grep+awk+sed
# 不过现在都有运维平台了，我们这边日志都落到了ES，所以用的少了
```

```
# 找到当前运行的vim程序并关闭
ps aux | grep vim | grep -v grep | awk '{print $2}' | xargs kill
```

```
# https://www.kernel.org/doc/Documentation/filesystems/proc.txt

# 使用grep查找Pss指标后，再用awk计算累加值
$ grep Pss /proc/[1-9]*/smaps | awk '{total+=$2}; END {printf "%d kB\n", total }'
```

```
# 对imaginingme.cn进行网络通信检查
ping imaginingme.cn | awk 'match($0, /time=(.*)ms|timeout/) { print (RLENGTH > 7)  ? substr($0, RSTART+5, RLENGTH-8) : 9999; fflush() }'
```

### 推荐书籍
- http://linux.vbird.org/linux_basic/
可以在线查找，是繁体的