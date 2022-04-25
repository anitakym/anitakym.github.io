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


#### Network Time Proctocol - NTP
- 如果系统时间存在误差，可以起Cron任务，配置NTP服务，定时同步
```
rpm -q ntp
yum -y install ntp
systemctl enable ntpd
systemctl start ntpd
```

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

#### fx
- https://github.com/antonmedv/fx
```
fx data.json
# 不展开
curl ... | fx # 点击可展开，可搜索 .xxx.xxx
# 全部展开
curl ... | fx .
```
- 查问题的时候，能方便看到json数据
#### wget
Wget - The non-interactive network downloader.


#### netstat
```
netstat -- show network status
# 查看连接当前服务器的用户IP，前5名
netstat -nat | awk '{print $5}' | awk -F ':' '{print $1}' | sort | uniq -c | sort -rn | head -n 5

```



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
- tail 默认最后10行
- tail -f(循环读取)

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


### 定时任务
```
cron - 周期性执行
at - 单一时刻执行一次任务

```

### /etc/init.d


## 名词解释
> man XXX / xxx --help 

1. su / sudo (man su / man sudo)  su 使用的是root的密码，sudo使用的是当前用户的密码
2. default setting 默认设置
3. enable adapter  授权适配
4. at the boot prompt (boot:引导，启动)
5. sed：stream editor for filtering and transforming text
   ```
   A stream editor is used to perform basic text transformations on an input stream (a file or
     input from a pipeline).  While in some ways similar to an editor which permits scripted edits (such as ed),  sed  works by  making only one pass over the input(s), and is consequently more efficient.  But it is sed's ability to filter text
     in a pipeline which particularly distinguishes it from other types of editors.
    ```
特点：1、非交互式编辑器；
     2、没有破坏性，不修改原文件，除非使用shell的重定向符来保存结果；
     3、sed也支持sed脚本。
其工作原理为：将一行文字读到内存空间（该内存空间称为sed的模式空间）里面去，做完处理之后，再输出到屏幕上。
sed 的模式空间：即能被sed匹配到的字符串被存放到的内存空间。
6. command prompt 命令提示符;
7. subsystem 子系统，分系统;
8. X11 forwarding 
9. 动态主机配置协议（Dynamic Host Configuration Protocol, DHCP）是一个局域网的网络协议，使用UDP协议工作，主要有两个用途：给内部网络或网络服务供应商自动分配IP地址，给用户或者内部网络管理员作为对所有计算机作中央管理的手段。
10. SSH 为 Secure Shell 的缩写，由 IETF 的网络工作小组（Network Working Group）所制定；SSH 为建立在应用层和传输层基础上的安全协议。SSH 是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。SSH最初是UNIX系统上的一个程序，后来又迅速扩展到其他操作平台。SSH在正确使用时可弥补网络中的漏洞。SSH客户端适用于多种平台。几乎所有UNIX平台—包括HP-UX、Linux、AIX、Solaris、Digital UNIX、Irix，以及其他平台—都可运行SSH。
11. archive 归档



<pre>
su：Swith user  切换用户，切换到root用户
cat: Concatenate  串联
uname: Unix name  系统名称
df: Disk free  空余硬盘
du: Disk usage 硬盘使用率
chown: Change owner 改变所有者
chgrp: Change group 改变用户组
ps：Process Status  进程状态
tar：Tape archive 解压文件
chmod: Change mode 改变模式
umount: Unmount 卸载
ldd：List dynamic dependencies 列出动态相依
insmod：Install module 安装模块
rmmod：Remove module 删除模块
lsmod：List module 列表模块
alias :Create your own name for a command
bash :GNU Bourne-Again Shell  linux内核 
grep:global regular expression print
httpd :Start Apache
ipcalc :Calculate IP information for a host
ping :Send ICMP ECHO_Request to network hosts
reboot: Restart your computer
sudo:Superuser do
 
/bin = BINaries 
/dev = DEVices 
/etc = ETCetera 
/lib = LIBrary 
/proc = PROCesses 
/sbin = Superuser BINaries 
/tmp = TeMPorary 
/usr = Unix Shared Resources 
/var = VARiable ? 
FIFO = First In, First Out 
GRUB = GRand Unified Bootloader 
IFS = Internal Field Seperators 
LILO = LInux LOader 
MySQL = My最初作者的名字SQL = Structured Query Language 
PHP = Personal Home Page Tools = PHP Hypertext Preprocessor 
PS = Prompt String 
Perl = "Pratical Extraction and Report Language" = "Pathologically Eclectic Rubbish Lister" 
Python Monty Python's Flying Circus 
Tcl = Tool Command Language 
Tk = ToolKit 
VT = Video Terminal 
YaST = Yet Another Setup Tool 
apache = "a patchy" server 
apt = Advanced Packaging Tool 
ar = archiver 
as = assembler 
bash = Bourne Again SHell 
bc = Basic (Better) Calculator 
bg = BackGround 
cal = CALendar 
cat = CATenate 
cd = Change Directory 
chgrp = CHange GRouP 
chmod = CHange MODe 
chown = CHange OWNer 
chsh = CHange SHell 
cmp = compare 
cobra = Common Object Request Broker Architecture 
comm = common 
cp = CoPy 
cpio = CoPy In and Out 
cpp = C Pre Processor 
cups = Common Unix Printing System 
cvs = Current Version System 
daemon = Disk And Execution MONitor 
dc = Desk Calculator 
dd = Disk Dump 
df = Disk Free 
diff = DIFFerence 
dmesg = diagnostic message 
du = Disk Usage 
ed = editor 
egrep = Extended GREP 
elf = Extensible Linking Format 
elm = ELectronic Mail 
emacs = Editor MACroS 
eval = EVALuate 
ex = EXtended 
exec = EXECute 
fd = file descriptors 
fg = ForeGround 
fgrep = Fixed GREP 
fmt = format 
fsck = File System ChecK 
fstab = FileSystem TABle 
fvwm = F*** Virtual Window Manager 
gawk = GNU AWK 
gpg = GNU Privacy Guard 
groff = GNU troff 
hal = Hardware Abstraction Layer 
joe = Joe's Own Editor 
ksh = Korn SHell 
lame = Lame Ain't an MP3 Encoder 
lex = LEXical analyser 
lisp = LISt Processing = Lots of Irritating Superfluous Parentheses 
ln = LiNk 
lpr = Line PRint 
ls = list 
lsof = LiSt Open Files 
m4 = Macro processor Version 4 
man = MANual pages 
mawk = Mike Brennan's AWK 
mc = Midnight Commander 
mkfs = MaKe FileSystem 
mknod = MaKe NODe 
motd = Message of The Day 
mozilla = MOsaic GodZILLa 
mtab = Mount TABle 
mv = MoVe 
nano = Nano's ANOther editor 
nawk = New AWK 
nl = Number of Lines 
nm = names 
nohup = No HangUP 
nroff = New ROFF 
od = Octal Dump 
passwd = PASSWorD 
pg = pager 
pico = PIne's message COmposition editor 
pine = "Program for Internet News & Email" = "Pine is not Elm" 
ping =  Packet InterNet Grouper 
pirntcap = PRINTer CAPability 
popd = POP Directory 
pr = pre 
printf = PRINT Formatted 
ps = Processes Status 
pty = pseudo tty 
pushd = PUSH Directory 
pwd = Print Working Directory 
rc = runcom = run command, shell 
rev = REVerse 
rm = ReMove 
rn = Read News 
roff = RunOFF 
rpm = RPM Package Manager = RedHat Package Manager 
rsh, rlogin, = Remote 
rxvt = ouR XVT 
sed = Stream EDitor 
seq = SEQuence 
shar = SHell ARchive 
slrn = S-Lang rn 
ssh = Secure SHell 
ssl = Secure Sockets Layer 
stty = Set TTY 
su = Substitute User 
svn = SubVersioN 
tar = Tape ARchive 
tcsh = TENEX C shell 
telnet = TEminaL over Network 
termcap = terminal capability 
terminfo = terminal information 
tr = traslate 
troff = Typesetter new ROFF 
tsort = Topological SORT 
tty = TeleTypewriter 
twm = Tom's Window Manager 
tz = TimeZone 
udev = Userspace DEV 
ulimit = User's LIMIT 
umask = User's MASK 
uniq = UNIQue 
vi = VIsual = Very Inconvenient 
vim = Vi IMproved 
wall = write all 
wc = Word Count 
wine = WINE Is Not an Emulator 
xargs = eXtended ARGuments 
xdm = X Display Manager 
xlfd = X Logical Font Description 
xmms = X Multimedia System 
xrdb = X Resources DataBase 
xwd = X Window Dump 
yacc = yet another compiler compile

</pre>

<pre>
EOF = end of file(https://en.wikipedia.org/wiki/End-of-file)
RPC = Remote Procedure Call(Remote Procedure Call (RPC) is a protocol that provides the high-level communications paradigm used in the operating system.)
</pre>
