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
