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