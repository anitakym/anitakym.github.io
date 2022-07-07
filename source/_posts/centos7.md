---
title: centos7
date: 2021-10-06 13:50:26
tags:
---
## history
Unix（FreeBSD） - 贝尔实验室
Minix - 安德鲁
Linux - Linus Torvalds - (Redhat -> Centos | Ubuntu )

## 使用率

## basic
#### 基础变更
- 文件系统 - xfs
- /etc/hostname - 修改主机名 | timedatectl set-timezone - 时区设置 | ip - ip信息查看| ss - 端口查看 ｜ firewalld - 防火墙 | systemd - 服务管理 ｜ chrony - 时间同步
- 默认支持docker - 内核支持：OverlayFS ｜ Repo源支持
- 不再支持32位操作系统
- GNOME 3.x
- centos7 - systemd 不断完善，强大 (ubuntu等也在不断加强使用)

#### hostname
```
vim /etc/hostname
直接改里面的名字
reboot # reboot 之后，永久修改才会生效
```

#### file | dir
- 树状结构
```
/bin = User BINaries 
/sbin = Superuser BINaries 
/etc = ETCetera - configuration files
/dev = DEVices files
/proc = PROCesses information - top命令
/lib = LIBrary - system libraries
/tmp = TeMPorary 
/usr = Unix Shared Resources  - user programs
/boot = Boot loader files
/var = VARiable 
/opt = optional add-on apps
/mnt = mount directory
/media = removable devices
/src = service data
```
有时候查问题的时候，注意6/7的文件目录结构的变更
- bin -> usr/bin (7链接到了usr/bin下)
- sbin -> usr/sbin
- lib | lib64 等同上
- centos7 里面多了run目录
```
cd /;ls ./
```

#### timezone
- 中国 - +8
- 时区不准确，会导致系统时间有问题，即使配置了时间同步
```
date -R
cat /etc/local
cat /ect/localtime
time
timedatectl # ntp的协议进行时间同步的｜RTC - 本地主板时间
timedatectl set-timezone Asia/Shanghai
timedatectl set-local-rtc 1 # 将硬件时间调整成和本地时间（local time zone）一致
```

#### 网络接口
- 默认命名规则
- centos6，如果是Dell的，可能会有em0等出现
- centos7 - net.ifnames 命名全自动，可预知，但是命名比较难读 ｜ biosdevname = 提供给Dell部分
- /etc/sysconfig/grub -> GRUB_CMDLE_LINUX
- ifconfig - 阿里云的有这个命令，这个命令在（centos7-minimal安装）里面就默认没有了
- ip还是很强大的，推荐使用
```
ip a # a - addr 
ip a add|del # 修改ip地址信息
ip link set dev eth1 down|up # 关闭｜启用网络接口
# 策略路由配置
```

#### 自动补全
- tab （一下｜两下）
- 名字 ｜ 参数 - 安装bash-completion,然后重新登入主机

#### 系统内存
- 操作系统内存 - 应用程序 ｜ buffers ｜ cached ｜ 未使用
- shared 是很小的，不同程序间的共享内存
- Buffers - 存储速度｜优先级 - 不同的设备之间传输数据的缓存区域
- Cached - CPU读取数据文件缓存的存储缓存区域
- Buffers ｜ Cache 部分可以回收，来提供给应用程序使用
- 操作系统内存耗尽，触发OOM机制（out of memory），导致系统自动重启
- swap原理要理解 - 操作系统内存不够，会用swap -其实解决不了根本问题- mongoDB等还会产生问题
- Used到60%-80% 要注意
```
top # 1 | shift + M | shift + P
free # 内存
free -m # 单位 M，free是未被分配的内存，Used-应用程序使用的
```

#### 端口状态查看
```
# ss - centos7 - 执行快（比netstat）- /proc/net/
# netstat - centos6 - /proc/-遍历
# ECS里面这两个默认都有
netstat|ss -luntp # 查看正在监听的端口
netstat -an | grep 80 # 查看使用某个端口的情况
# umount /proc/ -l 再用netstat或者ss，就会提示，提取不到信息了
ss -ltn # 查看tcp对应的
ss -lun # 查看udp对应的
# ss 可以通过各种参数配置，查看各种状态，判断问题
ss state established | wc -l
ss -s # 概览，做一个大概判断 ｜ synrecv如果很高，可能遭受攻击
ss -an sport eq 22
```

#### TCP
- listen | established | fin_wait1 | close_wait | fin_wait2 |last_ack | "time_wait" | closed
- syn_sent | syn_recv
- 三次握手｜四次挥手

## Systemd
#### basic
- Systemd - centos7 - 新采用的管理体系，对比sysVini(centos6)
- 服务管理｜启动项管理｜系统启动级别｜定时任务｜日志管理
- centos6 - service|chkconfig|init|cron|syslog
- centos7 - systemctl|systemctl|systemctl|timer|Systemd-journal
- 支持并行启动
```
# 可以提高开机启动速度(case，找一台中间机器，比较下速度)
yun install vsftpd
# 对于不同的6,7的，进行reboot，从中间机器上，看下联通情况
systemctl enable vsftpd # 加入开机启动-7
chkconfig vsftpd on # 加入开机启动-6

watch 'echo exit|nc xxx.xxx.xxx.xxx 21' # 中间机器
```
- centos7 关机只关闭正在运行的服务
- 对于服务的挂历不需要init.d下的脚本
- Service ｜ Syslog - 原有问题解决

#### systemctl
- 文件扩展名 - 管理单元
```
systemctl -t help # 查看支持哪些单元的管理
df -h
systemctl list-unit | grep 'boot' 
systemctl start|stop nginx # service
```
- 如果无扩展名，systemctl默认会把扩展名当成.service
- `systemctl list-units | --failed | list-unit-files | deamon-reload`
- 单元管理命令 - start|stop|restart|reload|status|is-enabled
- 基本命令 enable|disable|mask|unmask
- systemctl [options] command [name]
- systemctl -h

#### target 
- SysVinit vs Systemd
- 系统启动运行级别 - 0～6
```
# SysVinit
cat /etc/rc.d/rc3.d
runlevel
init|telinit 6 # 非永久
# Systemd
systemctl get-default
systemctl set-default|isolate xxx.target
reboot
```
- `systemctl list-dependencies` # 看到关联关系
- `systemctl --reverse list-dependencies xxx.service`

#### service
```
# SysVinit
service name start|stop|restart|reload|status|condrestart
# Systemd
systemctl start|stop|restart|reload|status|condrestart name
```
```
rpm -ql nginx
rpm -qa nginx
vim nginx.service
systemctl start nginx.service
systemctl status nginx.service
systemctl reload nginx.service # 不希望重启，只是重载下配置文件，这样几乎不会影响用户访问
systemctl restart nginx.service # 如果有用户正在使用，会有影响
cat nginx.service 或 systemctl cat nginx
# [unit] - 单元的说明及依赖相关的设置 (wants|requires区别)
# [service] - define - 单元的管理方式(type=simple-该服务将立刻启动|forking-当该服务进程fork,且父进程退出后服务启动成功｜oneshot|notify|dbus|idle)
# [install] - define - 加入到target单元中
```
- 软件包安装的单元 - /usr/lib/systemd/system/
- 系统管理员安装的单元 - /etc/systemd/system/

#### 自定义服务单元
```
#!/bin/bash

echo $$ > /var/run/xxx.pid
while :
do 
    echo "hello,"$(date) >> /tmp/xxx.res
    sleep 1
done
```
```
tail -f /tmp/xxx.res
cp nginx.service xxx.service # 改一下拷过来的配置文件
# :! ls /path 可以测试路径是否正确
```
```
systemctl daemon-reload # 每次改完配置文件，要reload
```

#### Timers
- 替代cron,定时控制服务事件（.service文件）
- 定时任务 = service服务单元 + timer定时单元
- 单调定时器 - 从一个时间点过一段时间后激活定时任务｜ 实时定时器 - 类比crontab(OnCalendar=*-*-* 00:00:00)
- [Unit][Timer][Install]
- https://fedoramagazine.org/systemd-timers-for-scheduling-tasks/
```
systemctl list-timers
```

#### Journal
- Systemd的日志管理
- /etc/systemd/journald.conf
- RAM - tmpfs /run (df -h)
- /run/log/journal/  - 重启之后不会存在
- ```journalctl```
- 操作系统日志级别 - 0～7
- `journalctl [options] [matches]`
- notice|warning - 粗体 error-红色
- `journalctl -n` # -n最后20行, -f实时，-p级别,-u具体单元

#### Firewalld
- https://firewalld.org/
- iptables - centos6
- 底层调用的iptables
- 区域管理
- 默认区域 - public
- 活跃｜非活跃 区域
- ls /usr/lib/firewalld/zones/
- systemctl start firewalld.service
- `fiewall-cmd --list-all`
- `ip a`
- 外部访问服务器，默认阻止，服务器访问外部默认允许
```
# 一个网卡接口只能属于一个zone,一个zone可以有多个网卡接口
# 配置了网络接口的区域是活跃区域（或者源地址配置add-source）
systemctl status
ip a
firewall-cmd --get-active-zones
```
```
# 端口白名单配置
ss -lntp
telnet xxx.xxx.xx.x 21 # 本机测试端口连通性
firewall-cmd --zone=public --add-port=21/tcp
firewall-cmd --list-all
firewall-cmd --reload # 动态加载新规则，在规则修改后，要执行这个，来使规则生效
firewall-cmd --complete-reload
firewall-cmd --zone=public --add-port=21/tcp --permanent
# 服务白名单配置
firewall-cmd --zone=public --add-service=http
```
- 区域规则结合，可以得出想要的最终配置
```
# default 设置为drop
firewall-cmd --zone=trusted --add-source=xxx.xxx.xxx.xx/24
```

## 文件系统
#### 基本
- 装载 - 分区 - 格式化 => 文件系统
- c6 - ext4,ext3,ext2   c7 - xfs  c7-ecs-ext4
- xfs - 扩展性支持能力高于ext4

#### 云盘
- ECS存储空间
- 数据隔离
- 提升性能

- /dev/vda ext4 /系统目录
- /dev/vd* xfs /应用目录
- fdisk /dev/vdb
- mount 

