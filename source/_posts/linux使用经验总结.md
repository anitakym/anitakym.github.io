---
title: linux使用经验总结
date: 2020-08-06 16:44:03
tags:
    - Linux系统使用系列
---
### 学习参考资料
https://github.com/jlevy/the-art-of-command-line/blob/master/README-zh.md
- the-art-of-command-line


### 报错解决

```
touch h(1).txt
```
- -bash: syntax error near unexpected token `('
- zsh: no matches found: 嘿嘿(1).txt
因为括号的原因啦，需要转义，加\; 也可以加引号；


> 一些和系统平台无关的command

#### !$，表示上一个命令行的最后一个参数。

#### !!，表示上一个命令的完整命令

#### gzip
平时构建出来的文件，想看看gzip之后大小
```gzip xxx.js```

#### tree
```
man tree
```
mac 上想使用，用brew安装
(比tree更好看的是 [exa](https://the.exa.website/install/macos))

- 场景（查看项目里面的文件，排除node_modules）
```
tree - I "node_modules" -f | grep -C3 index.md
```
也可以用把结果输出后，用编辑器进行更复杂的搜索
#### chmod
```
chmod -R 777 
```
设置当前目录及子目录所有文件=>所有人可读写可执行

#### cp
```
cp -r /root/firekylin/www/static/pic /root/firekylin_1.x/www/static/pic 
```

#### z
文件夹跳转

#### vidir
可以批量修改文件名

#### grep
cat del2.log | grep  -oP "\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*" > del3.log


#### 命令行操作
<pre>
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

所以：
Ctrl + a
Ctrl + k
删除一整行
</pre>

#### top
这个是个蛮重要的，一般机器情况看下这个基本上就知道了(Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况)

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

Mac上面，<strong>“活动监视器是”</strong>GUI的面板
Windows,类似于任务管理器。



#### nohup
参考资料：https://developer.ibm.com/zh/tutorials/l-lpic1-103-5/

#### curl
curl - transfer a URL
curl  is  a tool to transfer data from or to a server, using one of the supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  IMAP, IMAPS,  LDAP,  LDAPS,  POP3,  POP3S,  RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET and TFTP).
cURL是一个多功能工具。当然，它可以下载网络内容，但同时它也能做更多别的事情。

curl is powered by  libcurl  for  all  transfer-related  features.
cURL 技术支持库是：libcurl。这就意味着你可以基于 cURL 编写整个程序，允许你基于 libcurl 库中编写图形环境的下载程序，访问它所有的功能。

curl offers a busload of useful tricks like proxy support, user authentication, FTP upload, HTTP post, SSL connections, cookies, file  transfer  resume,  Metalink,  and more.
cURL 宽泛的网络协议支持可能是其最大的卖点。cURL 支持访问 HTTP 和 HTTPS 协议，能够处理 FTP 传输。它支持 LDAP 协议，甚至支持 Samba 分享。实际上，你还可以用 cURL 收发邮件。

cURL 也有一些简洁的安全特性。cURL 支持安装许多 SSL/TLS 库，也支持通过网络代理访问，包括 SOCKS。这意味着，你可以越过 Tor 来使用cURL。
cURL 同样支持让数据发送变得更容易的 gzip 压缩技术。

#### wget
Wget - The non-interactive network downloader.


#### netstat
netstat -- show network status


#### alias
自定义指令
注意，如果使用了zsh,则改动bash的配置就不生效了,只需要处理下.zshrc文件即可
```
open -e .zshrc 
source .zshrc
```

#### fx(https://github.com/antonmedv/fx)
能够格式化JSON文本
#### 日志
tail/lnav

### 具体场景
####  查看目录下文件/文件夹个数
```
# 文件
_posts git:(master) ✗ ls -l | grep "^-" | wc -l
     149
# 文件夹
_posts git:(master) ✗ ls -l | grep "^d" | wc -l
     135

# 包括子文件夹
ls -lR
```

### export
Linux export 命令用于设置或显示环境变量。

在 shell 中执行程序时，shell 会提供一组环境变量。export 可新增，修改或删除环境变量，供后续执行的程序使用。export 的效力仅限于该次登陆操作。
```
export [-fnp][变量名称]=[变量设置值]
```

### 基本操作
```
date | cal | df | free( free - Display amount of free and used memory in the system 显示内存使用情况的统计信息)
[root@VM-12-3-centos ~]# free
              total        used        free      shared  buff/cache   available
Mem:        1882008      501288       80272         520     1300448     1196596
[root@VM-12-3-centos ~]# df -Th
Filesystem     Type      Size  Used Avail Use% Mounted on
devtmpfs       devtmpfs  908M     0  908M   0% /dev
tmpfs          tmpfs     919M   24K  919M   1% /dev/shm
tmpfs          tmpfs     919M  496K  919M   1% /run
tmpfs          tmpfs     919M     0  919M   0% /sys/fs/cgroup
/dev/vda1      ext4       59G  5.9G   51G  11% /
tmpfs          tmpfs     184M     0  184M   0% /run/user/0
[root@VM-12-3-centos ~]# df -Th /data
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/vda1      ext4   59G  5.9G   51G  11% /

# -h (--human) 方便阅读的数据单位格式
# -T (--print-type) print file system typeq
```
free里面有个buffer(缓冲区)，例如打印场景；在Linux中，你会发现系统运行的时间越长，占用的内存就越多。这并不是说Linux用完了所有内存，而是Linux利用所有的可用内存尽可能地进行缓冲；
卸载设备会将所有剩余的数据写入设备，以便能够将其安全地移除。如果在移除前没有先卸载，则存在数据并未完全写入该设备的可能性。
### 存储介质
mount：挂载文件系统
umount：卸载文件系统
fsck：检查和修复文件系统
fdisk：操作分区
mkfs：创建新的文件系统
dd：转换和复制文件
genisoimage（mkisofs）：创建ISO 9660映像文件
wodim（cdrecord）：擦除和刻录光学存储介质
md5sum：计算MD5校验和