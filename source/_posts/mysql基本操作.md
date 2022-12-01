---
title: mysql基本操作
date: 2020-01-06 16:52:15
tags:
    - mysql
---

### 客户端/服务端
- MySQL数据库实例 - 代表着MySQL服务器程序的进程
- mysqld - 启动的MySQL服务器进程的默认名称
- mysql - 客户端进程的默认名称
### 安装
- 安装目录
```
macos(类unix)
/usr/local/mysql
win
C:\Program Files\MySQL\MySQL Server 8.0
```

### bin目录下的可执行文件
- 将该bin目录的路径加入到环境变量PATH中

### 启动MySQL服务器程序
- unix里启动服务器程序
- mysqld
- mysqld_safe
- mysql.server
- mysqld_multi

### 启动MySQL客户端程序
- mysql | mysqldump | mysqlcheck | mysqladmin ...
- `mysql>` 客户端提示符
- 断开客户端与服务器的连接并且关闭客户端（quit， exit，\q）

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

#### ER_NOT_SUPPORTED_AUTH_MODE
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
ALTER USER 'root' IDENTIFIED WITH mysql_native_password BY '123456';
```

### 数值类型
#### 整数类型 
- 进制
- 8个比特位代表一个字节
- 用若干个字节表示一个证书

#### MySQL的整数类型
- 类型
- 占用的存储空间（单位：字节）
- 无符号数值的取值范围
- 有符号数取值范围（有符号数需要一个比特位表示正负号）
- 含义

#### 浮点数类型
- 符号部分 指数部分 尾数部分
- 类型
- 占用的存储空间（单位：字节）
- 绝对值最小非0值
- 绝对值最大非0值
- 含义
- FLOAT | DOUBLE
- 更多的小数是无法直接转换成二进制的，比如0.3，它转换成的二进制小数就是一个无限小数，所以只能进行一些舍入来近似表示，所以计算机的浮点数有时是不精确的
- 设置最大位数和小数位数 FLOAT（M，D） DOUBLE（M，D）
- M表示该小数最多需要的十进制有效数字个数，D表示该小数的小数点后的十进制数字个数
- M和D都是可选的，如果省略了，它们的值按照机器支持的最大值来存储


### binlog
- binlog日志文件 
- 前四个字节固定的： 0xfe626963
- 由若干个事件构成的
- 事件1 - 格式描述事件format description event
- 事件 - event header | event data
- 基于语句statement和基于行row的binlog


## 数据库管理工具
- MySQL workbench
- dbeaver - https://github.com/dbeaver/dbeaver