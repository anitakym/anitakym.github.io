---
title: map和forEach使用指北
date: 2020-10-21 13:05:31
tags:
---
### forEach
`Array.prototype.forEach()` 是 JavaScript 中数组迭代的一种方法。`forEach()` 方法对数组的每个元素执行指定的操作，通常使用函数作为参数。它不会返回新数组，仅用于数组元素的操作和迭代。

以下是使用 `arr.forEach()` 的最佳实践：

1. 函数参数

当使用 forEach() 时，传递一个函数作为参数。该函数可以是一个命名函数或箭头函数，这取决于你的需求和喜好。 箭头函数使语法更简洁，但请注意，它们不绑定自己的 `this`，有时这可能会导致问题。

```javascript
// 使用箭头函数
arr.forEach((element) => {
  console.log(element);
});

// 使用命名函数
function processElement(element) {
  console.log(element);
}

arr.forEach(processElement);
```

2. 接收可以传递给回调函数的额外参数

forEach() 的回调函数还可以接收第二个参数，即当前元素的索引。 这可以帮助你在需要时检查数组的迭代状态。

```javascript
arr.forEach((element, index) => {
  console.log(`Element at index ${index} is: ${element}`);
});
```

3.不要在迭代过程中修改原始数组

使用 forEach() 迭代时不要修改原始数组。这可能会导致意料之外的结果。 如果需要改变原始数组，请考虑使用其他数组方法，如 map() 或 filter()。

```javascript
// 不推荐：在迭代过程中修改原始数组
arr.forEach((element, index) => {
  arr[index] *= 2;
});

// 推荐：使用 map() 创建新数组
const newArr = arr.map((element) => element * 2);
```

4. 使用 `thisArg` 参数

forEach() 还支持第二个参数 `thisArg`，这允许你为回调函数绑定 `this`。使用时需小心，因为箭头函数和其他类型的回调可能有不同的行为。

```javascript
const myObj = {
  counter: 0,
  incrementCounter: function(num) {
    this.counter += num;
  },
};

const numbers = [1, 2, 3, 4, 5];
numbers.forEach(function(num) {
  this.incrementCounter(num);
}, myObj);


5. 错误处理

使用 `Array.prototype.forEach()` 时，注意处理回调中可能抛出的异常。当你需要捕获异常时，可以在回调函数内部使用 try-catch。

```javascript
arr.forEach((element, index) => {
  try {
    // Your code here, it might throw an error
  } catch (error) {
    console.error(`Error processing element at index ${index}: ${error.message}`);
  }
});
```

综上，这些最佳实践有助于你更有效地使用 Array.prototype.forEach() 进行数组迭代。


### map
- 当我们需要对数组内容做批量修改、同时修改的逻辑又高度一致时，就可以调用 map 来达到我们的目的


### for
- 从性能上看，for 循环遍历起来是最快的


### 数组初始化

#### 一维-fill
- 当给 fill 传递一个入参时，如果这个入参的类型是引用类型，那么 fill 在填充坑位时填充的其实就是入参的引用

#### 二维数组初始化
- for