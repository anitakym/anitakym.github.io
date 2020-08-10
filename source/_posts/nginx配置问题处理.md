---
title: nginx配置问题处理
date: 2020-08-03 16:46:32
tags:
    - nginx
---
> nginx（Engine X） 高性能的web服务器
  排名指路：https://w3techs.com/technologies/cross/web_server/ranking
  官网指路：http://nginx.org/en/

<pre>
轻量级： CPU，内存占用少（工作模式：进程池 + 单线程 => 消除了进程，线程切换的成本）
One master and several worker processes; worker processes run under an unprivileged user;
（在进程之上，master进程用来管理进程池，监控进程，自动恢复发生异常的worker，保持进程池的稳定和服务能力）
cite: https://time.geekbang.org/column/article/117492
</pre>

#### nginx 怎么找
1. ps -ef | grep nginx (ps:显示系统进程)
2. whereis nginx 软件安装路径(whereis -- locate programs;The whereis utility checks the standard binary directories for the specified programs, printing out the paths of any it finds.The path searched is the string returned by the sysctl(8) utility for the ``user.cs_path'' string)
3. which nginx 运行文件所在路径(which -- locate a program file in the user's path;The which utility takes a list of command names and searches the path for each executable file that would be run had these commands actually been invoked.)
4. cd / && find - name 'nginx.conf'
nginx.conf => 基本的
vhost => 应用的

#### nginx 403
```
chmod -R 777
ps aux | grep "nginx: worker process" | awk '{print $1}'
```
<pre>
nginx 
root
</pre>

`vim nginx.conf`把 user  改成 root,即可;

#### firekylin nginx
```
ln -s /root/firekylin/nginx.conf /etc/nginx/conf.d/firekylin.conf
```
nginx.conf里面：


<pre>
~   #波浪线表示执行一个正则匹配，区分大小写

# location ~ /static/ {
# etag  on;
# expires  max;
# } 
</pre>

把     
<pre>
# etag  on;
# expires  max;
</pre>

都注释了，还是403

把`location ~ /static/ {}`
也注释了，就生效了

文档指路：http://nginx.org/en/docs/beginners_guide.html


#### kill nginx 服务
nohup = No HangUP
```
ps -ef|grep nginx
cd /usr/local/nginx/sbin
ls
./nginx -s reload

kill -QUIT 28761
nohup /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
tail -2000f nohup.out
ps -ef|grep nginx
```