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

MySQL 8 和 MySQL 5.7 是两个主要版本，它们在性能、功能、安全性和兼容性等方面有显著差异。以下是 MySQL 8 和 MySQL 5.7 的主要区别：


### 1. **性能改进**
- **MySQL 8**:
  - 引入了更高效的查询优化器，支持更复杂的查询计划。
  - 默认使用 `InnoDB` 的并行读写优化，提升了事务处理性能。
  - 支持持久化的自适应哈希索引（Persistent Adaptive Hash Index），减少重启后的性能损失。
  - 改进了 `JSON` 数据类型的性能。

- **MySQL 5.7**:
  - 性能较 MySQL 5.6 有提升，但与 MySQL 8 相比在复杂查询和高并发场景下稍逊。

---

### 2. **默认字符集**
- **MySQL 8**:
  - 默认字符集为 `utf8mb4`，支持完整的 Unicode，包括表情符号。
  
- **MySQL 5.7**:
  - 默认字符集为 `latin1`，需要手动配置为 `utf8mb4` 才能支持完整的 Unicode。

---

### 3. **窗口函数和公用表表达式 (CTE)**
- **MySQL 8**:
  - 支持窗口函数（如 `ROW_NUMBER()`、`RANK()` 等），用于分析性查询。
  - 支持公用表表达式（CTE），包括递归查询，简化复杂查询的编写。

- **MySQL 5.7**:
  - 不支持窗口函数和 CTE。

---

### 4. **JSON 支持**
- **MySQL 8**:
  - 增强了对 `JSON` 数据类型的支持，提供了更多的函数（如 `JSON_TABLE()`）用于解析和查询 JSON 数据。

- **MySQL 5.7**:
  - 首次引入了 `JSON` 数据类型，但功能较为基础。

---

### 5. **数据字典**
- **MySQL 8**:
  - 引入了统一的数据字典，所有元数据存储在 `InnoDB` 表中，而不是文件系统中。
  - 提升了元数据管理的性能和一致性。

- **MySQL 5.7**:
  - 元数据存储在文件系统中，管理效率较低。

---

### 6. **安全性**
- **MySQL 8**:
  - 默认启用了更安全的密码插件（`caching_sha2_password`）。
  - 支持角色管理（Roles），简化权限管理。
  - 支持 TLS 1.3，增强了网络通信的安全性。

- **MySQL 5.7**:
  - 默认使用 `mysql_native_password` 插件，安全性较低。
  - 不支持角色管理。

---

### 7. **GIS 功能**
- **MySQL 8**:
  - 增强了对地理空间数据（GIS）的支持，提供了更多的函数和性能优化。

- **MySQL 5.7**:
  - 引入了基础的 GIS 支持，但功能较为有限。

---

### 8. **分区表**
- **MySQL 8**:
  - 改进了分区表的性能和管理，支持更多的分区类型。

- **MySQL 5.7**:
  - 分区表功能较为基础，性能优化有限。

---

### 9. **其他功能改进**
- **MySQL 8**:
  - 支持隐式主键（Invisible Index），可以隐藏索引以优化查询性能。
  - 支持正则表达式的增强（基于 ICU 的正则表达式）。
  - 支持 `NOWAIT` 和 `SKIP LOCKED`，改进了锁机制。

- **MySQL 5.7**:
  - 功能较为基础，不支持上述改进。

---

### 10. **兼容性**
- **MySQL 8**:
  - 不完全向后兼容，某些语法和功能在 MySQL 8 中被移除或更改（如 `GROUP BY` 的默认行为更严格）。
  - 升级时需要注意兼容性问题。

- **MySQL 5.7**:
  - 向后兼容性较好，适合从 MySQL 5.6 升级。

---

### 总结
| 特性                     | MySQL 8                  | MySQL 5.7               |
|--------------------------|--------------------------|-------------------------|
| 默认字符集               | `utf8mb4`               | `latin1`               |
| 窗口函数和 CTE           | 支持                     | 不支持                 |
| JSON 功能                | 更强大                   | 基础支持               |
| 数据字典                 | 统一存储在 `InnoDB` 中   | 文件系统存储           |
| 安全性                   | 更高（`caching_sha2_password`） | 较低（`mysql_native_password`） |
| 性能                     | 更高                     | 较低                   |
| GIS 功能                 | 更强大                   | 基础支持               |
| 分区表                   | 改进                     | 基础支持               |

如果你需要更高的性能、更强大的功能和更好的安全性，建议使用 MySQL 8。但如果你的项目依赖于旧版本的功能或需要更好的兼容性，MySQL 5.7 可能更适合。