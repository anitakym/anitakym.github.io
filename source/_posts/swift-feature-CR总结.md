---
title: swift-feature-CR总结
date: 2022-01-13 17:03:07
tags:
---
### lazy
#### Swift - lazy
- Swift 中，lazy 属性的特点是：仅在“需要”时加载，并且仅加载一次
- lazy 属性只在被调用的时候初始化，所以在 lazy 属性的初始化器中是可以访问当前实例的存储属性的
```
private lazy var imagePicker: SSImagePickerController = {
        let picker = SSImagePickerController()
        return picker
    }()

```
#### Scala - lazy
- Scala -  ```lazy val```


#### 
