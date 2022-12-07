---
title: mysql8从入门到精通-精读
date: 2021-08-02 14:19:04
tags:
---
nodejs
Server version: 8.0.28 Homebrew
```
select User,plugin from user;
+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| mysql.infoschema | caching_sha2_password |
| mysql.session    | caching_sha2_password |
| mysql.sys        | caching_sha2_password |
| root             | caching_sha2_password |
+------------------+-----------------------+
4 rows in set (0.00 sec)
```
`2022-12-06 17:57:47,581 ERROR 35487 [-/127.0.0.1/-/0ms GET /] nodejs.ER_NOT_SUPPORTED_AUTH_MODEError: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client`

1.nodejs
egg-mysql -> ali-rds -> mysql(https://www.npmjs.com/package/mysql)
"ali-rds": {
      "version": "3.4.0",
      "resolved": "https://registry.npm.taobao.org/ali-rds/download/ali-rds-3.4.0.tgz",
      "integrity": "sha1-6rpDN4DaMtaAT9mle917Yv2J/iU=",
      "requires": {
        "co-wrap-all": "^1.0.0",
        "debug": "^2.2.0",
        "mysql": "^2.13.0",
        "pify": "^2.3.0"
      },
mysql:
PLUGIN_AUTH - Uses the plugin authentication mechanism when connecting to the MySQL server. This feature is not currently supported by the Node.js implementation so cannot be turned on. (Default off)

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'mypwd';`
```
mysql> select User,plugin from user;
+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| mysql.infoschema | caching_sha2_password |
| mysql.session    | caching_sha2_password |
| mysql.sys        | caching_sha2_password |
| root             | mysql_native_password |
+------------------+-----------------------+
4 rows in set (0.00 sec)
```

flush privileges; 还是 重启 mysql 服务