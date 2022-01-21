---
title: swift-feature-CR总结
date: 2022-01-13 17:03:07
tags:
---
### lazy
#### Swift - lazy
- Swift 中，lazy 属性的特点是：仅在“需要”时加载，并且仅加载一次
- lazy 属性只在被调用的时候初始化，所以在 lazy 属性的初始化器中是可以访问当前实例的存储属性的
- 如果是lazy变量，这意味着只有在用到该变量的时候，程序才会为我们创建它的实例
```
private lazy var imagePicker: SSImagePickerController = {
        let picker = SSImagePickerController()
        return picker
    }()

```
#### Scala - lazy
- Scala -  ```lazy val```


#### Kotlin - lazy 委托
- 几十年前，John McCarthy引入了短路求值来消除布尔逻辑中的冗余计算——如果在表达式之前对表达式的求值足以产生结果，则跳过表达式的执行。大多数编程语言都支持这个特性，程序员很快就会了解到这种方法的效率。Lazy（惰性）委托扩展了这种方法的范围
```
private val mIvTitle: ImageView by lazy {
            view.findViewById(R.id.interactive_iv_name)
        }

```