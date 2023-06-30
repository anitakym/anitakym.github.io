---
title: CodeAnalysis-部署与应用
date: 2023-06-30 10:03:43
tags:
---
在 CentOS 8 上，可以使用以下命令来查看有关计算机的信息：
1. 查看 CPU 信息：
```
lscpu
```
2. 查看内存使用情况：
```
free -h
```
3. 查看硬盘空间及使用情况：
```
df -h
```
4. 显示所有 PCI 设备：
```
lspci
```
5. 显示所有 USB 设备：
```
lsusb
```
6. 查看网卡信息：
```
ip addr show
```
或
```
nmcli device status
```
7. 查看操作系统版本：
```
cat /etc/centos-release
```
8. 查看运行的进程：
```
top
```
或
```
htop
```
（需要先安装 htop：`sudo dnf install -y htop`）
9. 查看已安装软件包：
```
dnf list installed
```
10. 查看系统负载：
```
uptime
```