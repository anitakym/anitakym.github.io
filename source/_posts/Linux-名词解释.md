---
title: Linux-名词解释
date: 2015-12-15 11:24:24
tags:
    - 很久以前系列
    - Linux系统使用系列
---
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
