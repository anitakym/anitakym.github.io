---
title: python-language层面-总结
date: 2021-10-11 11:36:04
tags:
---
> bytes are bytes; characters ara an abstraction;an immutable sequence of unicode characters is called a string;an immutable sequence of numbers-between-0-and-255 is called a bytes object;(dive into python3)
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

#### 字典 枚举
- Python的枚举是个类，其它的语言是个类型，有关键字
```
class VIP(Enum):
	YELLOW = 1

Print(VIP.YELLOW)
VIP.YELLOW 


VIP.YELLOW.value
VIP.YELLOW.name
# 枚举类型，名字，值

for v in VIP:
	print(v)

枚举类型不支持 > < 比较
```
- 表示类型：字典（数据结构），类（封装）

- 缺点：都是可变的，可以被更改（类型被确定下来之后，是不让更改的）没有防止相同标签的功能

- 枚举：如果值相同，第二个的标签就是第一个的别名了，遍历的时候，第二个就不会出现;想要得到第二个，遍历这个
```
for v in VIP.__members__.items():
	print(v)


for v in VIP.__members__:
	print(v)
```
- 数据库存储：值用数字
```
a = 1
print(VIP(a))
# 枚举转换
Enum
IntEnum
```

### 装饰器：
unique
@unique

- 枚举在python中的实现是单例模式，所以不能new

- 设计模式应该在实践中,设计模式防止代码乱变化


## 函数：
print()

round(1.234, 3)


help(round)

import this
The Zen of Python, by Tim Peters

函数：
1. 功能性
2.   隐藏细节
3.   避免编写重复的代码
组织代码，自定义函数

def 关键字定义一个函数

1.参数列表可以没有
2.return value ,如果没有，默认返回的是None

Import sys

sys.setrecursionlimit(100000)


可变参数

对函数的返回值没有类型限制（动态类型语言）

解构赋值（序列解包）： 接收返回结果

Python 中数字不能和字符串相加

（定义过程中：形参，调用过程中：实参）
代码的可读性
1. 必须参数
2. 关键字参数（c = add(y=3, x=2)）
（区别在于调用上，定义上一样的）（关键字参数也要满足必须参数）

3.  默认参数（定义和调用的时候：非默认参数不能放在默认参数后面）

## 面向对象
有意义的面向对象的代码

类，对象
实例化

class StudentHomeWork( ):


调用了类下面的方法

def fun(self):

类最基本的作用：封装代码

类只负责定义（刻画，描述）
运行和调用要放在类的外部

建议模块里面如果写类，就写类，对类的调用就不要放在这个模块了


函数，方法：
C,C++
Java, C#

方法：设计层面
函数：程序运行，过程式的一种称谓


变量出现在模块，就是称为变量
如果出现在类里面，就是数据成员


类和对象：

类是现实世界或思维世界中的实体在计算机中的反映
它将数据以及这些数据上的操作封装在一起

数据成员表现特征
方法刻画行为


当类被实例化后，就变成了一个具体的对象


def __init__():
不能返回除none之外的值
构造函数
初始化对象的属性（特征）

实例化的时候，自动调用构造函数

模块下的全局变量，模块下函数里的局部变量


类变量-和类相关联在一起
实例变量-和对象相关联在一起
在面向对象的角度思考这个问题

类是抽象的，对象是具体的

Student类就不要name,name应该是对象有的

保存对象的特征值：
self（对实例变量赋值要加self）

谁调用了这个方法，self就是调用的那个实例对象

实例方法：和对象实例相关联的，实例可以调用的方法，定义时要self（显胜于隐），调用时不用传的

其他语言可能会用this 
显胜于隐

动态语言，写起来简单，但是对一些机制理解不深刻，就容易有坑

student1.__dict__
Student.__dict__



python类
	变量
		类变量
		实例变量
	方法
		实例方法
		类方法
		静态方法
	构造函数
	成员的可见性
	面向对象3大特性	
		继承性
		封装性
		多态性

方法可以操作变量，大部分是用来操作变量的

实例方法描述类的行为
构造函数初始化类的各种特征的

实例方法访问类变量

self.__class__.sum1
Student.sum1

定义类方法：

@classmethod
def plus_sum(cls):
	pass


Student.plus_sum()

Python 中，对象可以调用类方法


静态方法，类方法

静态方法，和类和对象都没什么关系，不太推荐使用

类的内部调用，外部调用

## 包，模块，函数与变量作用域

高性能，封装性（可复用），抽象能力

包(文件夹) dll.jar
模块 .py
类
函数，变量

js:npm is the package manager for JavaScript and the world’s largest software registry. Discover packages of reusable code — and assemble them in powerful new ways



Find, install and publish Python packages with the Python Package Index


seven.c4
six.c4

命名空间

包下面可以有子包

__init__.py

import module_name
import t.c7 as m
包引用的方法机制也是为了解决引入的各种问题，方便我们使用


解释型语言——有顺序的
__pycache__ 提高python运行效率的，虚拟机

Vscode:
 Files.exclude
__pycache__

Py换行 \

或者加（）

From c9 import (a, b 
,c) 

系统内置类库（内置标准库）

clear  清屏vscode







批量导入库

__init__


系统思维

包和模块不会被重复导入的
避免循环导入

一旦导入，就会执行模块里面的代码，在导入阶段只会执行一次

入口文件的概念

## 工程
- vim ｜ vscode 插件
Python 
不强制；
不需要{}区分代码块，用的缩进

条件控制 if else
循环控制 while
分支 switch(python不是)

桌面端代码的加密比较重要

Python 不适合去空格的压缩

ACCOUNT
type_kind_level


看似变量的丢到模块里面，会导致识别为不应为变量
变量应该在函数或者模块里面

Pylint

Snippet

结构体-作用域

代码块里面的代码是同级别的

python 没有goto 

分支里面很多分支，典型面向过程

抽成函数，基本的抽象

elif 替代 switch
字典的方式替代 switch（比较好）

从终端输入的得到的是字符串

A,b 不可能同时为false

a or b

循环，解决问题的思维模式，甚至穷举

While（condition 不能是常量）（python 中有else）(递归)
For 遍历/循环 序列，集合，字典(break, continue)(range())

序列切片
B = a[0, len(a):2]
Print(b)

## concept
命名可读性

变量要有意义

变量存储在内存中的值。这就意味着在创建变量时会在内存中开辟一个空间。
基于变量的数据类型，解释器会分配指定内存，并决定什么数据可以被存储在内存中。
因此，变量可以指定不同的数据类型，这些变量可以存储整数，小数或字符。

保留关键字不能用作变量名
如type,print 等方法也不要用做变量名

值类型，引用类型（值可以改变）

Python id 显示内存地址

	1.	1，id() 内存地址2.==比较的是值3.is  比较的是内存地址    数字，字符串，有小数据池    int -5--256    str:1,不能有空格        2.长度不能超过20个字符        3.不能有特殊字符如：#@....


js取不到的，用chrome的heap snapshot，能看到一个等价的地址，但不是真实的内存地址。

回复 flcwl：
js不提供对内存的直接访问，debug工具也只提供到vm的虚拟内存空间，想要取到底层的进程虚拟内存空间，只有用gdb去调试引擎源代码：https://medium.com/fhinkel/de...


一、作用域链：函数在定义的时候创建的,用于寻找使用到的变量的值的一个索引,而他内部的规则是,把函数自身的本地变量放在最前面,把自身的父级函数中的变量放在其次,把再高一级函数中的变量放在更后面,以此类推直至全局对象为止.当函数中需要查询一个变量的值的时候,js解释器会去作用域链去查找,从最前面的本地变量中先找,如果没有找到对应的变量,则到下一级的链上找,一旦找到了变量,则不再继续.如果找到最后也没找到需要的变量,则解释器返回undefined。
二、内存回收机制：一个函数在执行开始的时候,会给其中定义的变量划分内存空间保存,以备后面的语句所用,等到函数执行完毕返回了,这些变量就被认为是无用的了.对应的内存空间也就被回收了.下次再执行此函数的时候,所有的变量又回到最初的状态,重新赋值使用.但是如果这个函数内部又嵌套了另一个函数,而这个函数是有可能在外部被调用到的.并且这个内部函数又使用了外部函数的某些变量的话.这种内存回收机制就会出现问题.如果在外部函数返回后,又直接调用了内部函数,那么内部函数就无法读取到他所需要的外部函数中变量的值了.所以js解释器在遇到函数定义的时候,会自动把函数和他可能使用的变量(包括本地变量和父级和祖先级函数的变量(自由变量))一起保存起来.也就是构建一个闭包,这些变量将不会被内存回收器所回收,只有当内部的函数不可能被调用以后(例如被删除了,或者没有了指针),才会销毁这个闭包,而没有任何一个闭包引用的变量才会被下一次内存回收启动时所回收。

>>> id(p)
16079976
>>> hex(id(p))
'0xf55c68'

#!/usr/bin/python

aList = [123, 'xyz', 'zara', 'abc'];
aList.append( 2009 );
print "Updated List : ", aList;
Updated List :  [123, 'xyz', 'zara', 'abc', 2009]


jQuery append()

Tuple 不可改变，有时候需要



Js:
2**9
512
Math.pow(x,y) // x的y次幂 x——底数,y——幂数

成员运算符

对象的三个特征
值，身份， 类型
==    is   isinstance

位运算符

表达式是运算符和操作数所构成的序列 (序列：有序的)
expression     operator   operand

从左向右 左结合

如果有 =
右结合

 
