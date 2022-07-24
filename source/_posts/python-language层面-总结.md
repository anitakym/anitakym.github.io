---
title: python-language层面-总结
date: 2021-10-11 11:36:04
tags:
---
## 开发指南
### google python style guide
- https://google.github.io/styleguide/pyguide.html

### PEP 8 -- Style Guide for Python Code
- https://www.python.org/dev/peps/pep-0008/
- flake8 ```pip install flake8```

## 推荐
### Jupyter Notebook
- vscode 插件
- https://github.com/jupyter/notebook
- The Jupyter notebook is a web-based notebook environment for interactive computing.
- https://jupyter-notebook.readthedocs.io/en/stable/

### SQLAlchemy
#### ORM
- Object-Relational Mapping
- ORM框架的作用 - 把数据库表的一行记录与一个对象互相做自动转换
- https://github.com/sqlalchemy/sqlalchemy
- nodejs的话就是mongoose(https://github.com/Automattic/mongoose)

### type -a python
- 找到python解释器的完整路径

## lib
#### contextlib
- https://pymotw.com/3/contextlib/index.html

## basic
### pythonic
- https://www.tiobe.com/
- Java 静态语言，有编译过程
- ES6出来后，对面向对象的支持改善了
- python动态语言，面向对象（思想），（现实到计算机的映射）的语言
- 缺点：慢
- 编译型：C，C++（源代码编译成机器码）
- 解释型：javascript, python
- Java,C#（编译成中间代码）
- 胶水语言（把C，C++编写的模块组合在一起）
- 回归语言的本质，享受语言本身的纯粹之美
### 基本数据类型
#### 数字 - Number
int 整型 | float 浮点 | bool 布尔 | complex 复数

#### 组
序列 - str | list | tuple (有序，可用下标索引来访问，切片操作[0,5])
集合 - set (无序，没有索引，不能切片)
字典 - dict(key:value 键值对)