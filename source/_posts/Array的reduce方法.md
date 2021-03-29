---
title: Array的reduce方法
date: 2021-03-16 17:37:41
tags:
---
### MDN文档指南：
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

### 使用实例
ListNode的数据结构，如果我想把一个数组，转成ListNode的结构：
```
// leetcode2.两数相加

/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
let sum = 324
let arr = [...sum.toString()]
arr.reduce((acc,v)=>({val: v, next: acc}), null)
```
### 参考阅读材料：
- 深入浅出RxJS——6.1.3:规约统计（虽然讲的是rxjs中的reduce，但是对理解JavaScript中的reduce很有帮助）
```
无论是JavaScript数组原生支持的reduce，还是RxJS中的reduce操作符，都接受一个函数参数，这个函数参数就是“规约函数”，规约函数的形式如下：
function(accumulation,current){
  //accumulation是当前累计值，current是当前数据
  //函数应该返回最新的累计值
}
reduce的功能就是对一个集合中所有元素依次调用这个规约函数，这个规约函数可以返回一个“累积”的结果，然后这个“累积”的结果会作为参数和数据集合的下一个元素一起成为规约函数下次被调用的参数，如此遍历集合中所有的元素，因为规约函数可以任意定义，所以最后得到的“累积”结果也就完全可定制。

程墨. 深入浅出RxJS (实战) (Chinese Edition) (Kindle Locations 2496-2502). Kindle Edition. 
```

- JavaScript高级程序设计——5.2.9缩小方法
```
ECMAScript5还新增了两个缩小数组的方法：reduce()和reduceRight()。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。
其中，reduce()方法从数组的第一项开始，逐个遍历到最后。
而reduceRight()则从数组的最后一项开始，向前遍历到第一项。
这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为缩小基础的初始值。
传给reduce()和reduceRight()的函数接收4个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

泽卡斯(Zakas. Nicholas C.). JavaScript高级程序设计(第3版) (图灵程序设计丛书) (Chinese Edition) (Kindle Locations 3555-3562). 人民邮电出版社. Kindle Edition. 
```

- 深入理解ES6
箭头函数和数组：
箭头函数的语法简洁，非常适用于数组处理。
诸如sort()、map()及reduce()这些可以接受回调函数的数组方法，都可以通过箭头函数语法简化编码过程并减少编码量。

刘振涛. 深入理解ES6 (Chinese Edition) (Kindle Location 1196). Kindle Edition. 
在线版本(https://leanpub.com/understandinges6/read#leanpub-auto-arrow-functions)

### 杂谈 

> 函数式编程的一个重要洞见就是，大部分操作都可以归结成列表转换，其中，最核心的列表转换就是 map、filter 和 reduce
> python中的正则表达参考了Perl，而内置函数lambada,map,reduce,filter等参考了lisp