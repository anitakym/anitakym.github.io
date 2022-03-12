---
title: algorithm-and-logic-practice
date: 2021-09-26 15:26:11
tags:
---
## 随便写写
#### 水仙花数

```
const n = 150
const m = 158
let rangeStart = n
let rangeEnd = m
let isIn = (element) => {
  let arr = element.toString().split('')
  arr.unshift(0)
  let res = arr.reduce((prev, cur) => {
    return prev + Math.pow(Number(cur), 3)
  })
  if (res == element) {
    return true
  } else {
    return false
  }

}
let getNarc = (rangeStart, rangeEnd) => {
  let arrayIn = []
  for (let index = n; index <= m; index++) {
    if (isIn(index)) {
      arrayIn.push(index)
    }
  }
  return arrayIn
};
let narcs = getNarc(n, m)
console.log(narcs)
```

## leetcode



## basic

排序（快排，选择，希尔，冒泡） 
堆栈，队列，链表 递归～～～本质，终止条件，参数的传递
波兰式和逆波兰式（1+2/3）

## Stack && Queue[kju:]
- Stack - FILO - Array || Linked List 
- Queue - FIFO - Array || Doubly Linked List
- MQ
- www.bigocheatsheet.com - time|space complexity

## 20 合法括号
```
function isValid(s: string): boolean {
    let stack : Array<string> = []
    const parent_map : Object = {
        ')': '(',
        ']': '[',
        '}': '{'
    }
    for(let i = 0; i< s.length; i++) {
        if(!parent_map[s[i]]) {
            stack.push(s[i])
        } else if(stack.length === 0 || stack.pop() !== parent_map[s[i]]) {
            return false
        }
    }
    return stack.length === 0
}
```
```
不讲武德解法，一旦遇到(),{},[] 就用replace到空串，do while，哈哈哈哈，复杂度高点
```

### 232 225 栈和队列的彼此实现

