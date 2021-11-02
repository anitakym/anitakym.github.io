---
title: mysql基本操作
date: 2020-01-06 16:52:15
tags:
    - mysql
---


### 重启服务：
```service mysqld restart```

### 当密码不记得的时候：
```vim /etc/my.cnf```
增加一行：```skip-grant-tables ```

### 增加用户：
```mysql -u root -h 127.0.0.1 -p```
```
show database;
use mysql;
select user,password,host from user;
create user 'test'@'%' indentified by 'test';
grant all privileges on firekylin.* to 'test'@'%' with grant option;
FLUSH PRIVILEGES;
```

### 删除某个库：
```drop database;```


```mysqladmin```


#### log_bin

### err
#### 
Mac上：ERROR 2002 (HY000): Can’t connect to local MySQL server through socket ‘/tmp/mysql.sock’ (2)
```
 which mysql 
 brew info mysql 
```