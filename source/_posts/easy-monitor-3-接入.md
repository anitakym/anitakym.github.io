---
title: easy-monitor-3-接入
date: 2021-11-23 15:34:01
tags:
---
### Doc
- https://www.yuque.com/hyj1991/easy-monitor/deployment



### pre
- https://stackoverflow.com/questions/50093144/mysql-8-0-client-does-not-support-authentication-protocol-requested-by-server
```
ALTER USER 'root' IDENTIFIED WITH mysql_native_password BY 'password';
```


## 服务部署
```
wget https://repo.mysql.com//mysql80-community-release-el8-1.noarch.rpm


mysql:

yum -y install nodejs
npm install -g n
yum install git -y

# 项目可以fork一下，把config.prod.js加一下，推上去
git clone https://github.com/X-Profiler/xprofiler-console
git clone https://github.com/X-Profiler/xtransit-manager
git clone https://github.com/X-Profiler/xtransit-server

wget https://repo.mysql.com//mysql80-community-release-el8-1.noarch.rpm
rpm -ivh mysql80-community-release-el8-1.noarch.rpm
yum install mysql-server

https://dev.mysql.com/doc/refman/8.0/en/linux-installation-yum-repo.html

service mysqld restart

grep 'temporary password' /var/log/mysqld.log
mysql -uroot -p
alter user 'root'@'localhost' identified by 'xxxxxxxxx';

根据centos是7还是8安装对应的mysql,如80的安装在centos7上面就会出现问题

# /usr/bin/mysqladmin -u root password 'xxxx'
mysql -h localhost -u root -p
> create database xprofiler_logs;
> create database xprofiler_console;

cd xtrainsit-console/db
mysql -uroot -pxxxxxxxxx; -h127.0.0.1 -D 'xprofiler_console' < ./init.sql

cd xtrainsit-manager/db
mysql -uroot -pxxxxxxxxx -h127.0.0.1 -D 'xprofiler_logs' < ./init.sql
mysql -uroot -pxxxxxxxxx -h127.0.0.1 -D 'xprofiler_logs' < ./date.sql



redis

wget http://download.redis.io/releases/redis-5.0.8.tar.gz
tar -xvf redis-5.0.8.tar.gz
mv redis-5.0.8 /usr/local
cd /usr/local/redis-5.0.8/
yum list gcc
yum list tcl
yum install gcc # 版本
yum install tcl # 版本
make MALLOC=libc
make test
cd src && make install
vim redis.conf # daemon yes
./src/redis-server ./redis.conf


nginx 增加域名
emconsole.xxx.cn
172.111.111.111 emconsole.xxx.cn

/usr/local/tengine/sbin/nginx -s reload
/usr/local/tengine/sbin/nginx -t 


进入到gitlab各个项目下面，npm start

```