---
title: linux使用经验总结
date: 2020-08-06 16:44:03
tags:
    - Linux系统使用系列
---
#### tree
man tree

mac 上想使用，用brew安装


#### chmod

cp -r /root/firekylin/www/static/pic /root/firekylin_1.x/www/static/pic 

#### grep
cat del2.log | grep  -oP "\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*" > del3.log


#### 命令行操作
Ctrl + a
Ctrl + k
删除一整行


Ctrl+b 或左箭头键 左移一个字bai符（移至前一个字符）du
Ctrl+f 或右箭头键 右移一个字符（移至后一个字符）
Ctrl+a 移至行首
Ctrl+e 移至行尾
Esc b 左移一个单词
Esc f 右移一个单词
Del 删除光标所在处的字符
Ctrl+d 删除光标所在处的字符
BACKSPACE或Ctrl+h 删除光标左边的字符
Ctrl+k 删除至行尾


#### top

- 改变画面更新频率
　　l - 关闭或开启第一部分第一行 top 信息的表示
　　t - 关闭或开启第一部分第二行 Tasks 和第三行 Cpus 信息的表示
　　m - 关闭或开启第一部分第四行 Mem 和 第五行 Swap 信息的表示
　　N - 以 PID 的大小的顺序排列表示进程列表（第三部分后述）
　　P - 以 CPU 占用率大小的顺序排列进程列表 （第三部分后述）
　　M - 以内存占用率大小的顺序排列进程列表 （第三部分后述）
　　h - 显示帮助
　　n - 设置在进程列表所显示进程的数量
　　q - 退出 top

