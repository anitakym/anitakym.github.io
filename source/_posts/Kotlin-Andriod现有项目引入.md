---
title: Kotlin-Andriod现有项目引入
date: 2022-01-18 16:18:59
tags:
---
> 最近看android项目的提交，发现，诶，kt文件多了起来，梳理下；


## 官方文档
- https://developer.android.com/kotlin/first

## 项目相关
### 背景介绍
现有的Android项目，用Java开发，有个老师之前用Kotlin，所以他负责的模块kotlin写的比较多



## 其他
### JS
- https://www.kotlincn.net/docs/reference/js-overview.html

### kotlin-android-extensions插件在较新的Kotlin版本中已被弃用，您现在需要使用viewBinding或dataBinding来替代。

移除kotlin-android-extensions插件的步骤如下：

1. 打开您项目根目录下的 `build.gradle`（或 `build.gradle.kts`）文件，找到该行并移除：
   ```gradle
   apply plugin: "kotlin-android-extensions"
   ```
   如果您使用的是 `build.gradle.kts`，移除：
   ```kotlin
   apply(plugin = "kotlin-android-extensions")
   ```

2. 找到 `dependencies` 下的 `implementation "org.jetbrains.kotlinx:kotlinx-android-extensions:$version"` 并移除。

3. 使用View Binding或Data Binding来替代。

例如，如果您要使用View Binding，需要在每个模块的 `build.gradle` 文件中启用它，如下所示：

```gradle
android {
    ...
    viewBinding {
        enabled = true
    }
}
```
然后更新你的代码来使用View Binding。这通常包括使用 `binding` 对象代替 `findViewById` 或Kotlin Android Extensions 的synthetic properties。例如：

```kotlin
class MyActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMyBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMyBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
        
        binding.myButton.setOnClickListener { /*...*/ }
    }
}
```

"kotlin-android-extensions" 和 "kotlin-android" 是Kotlin在Android中的两个不同插件，它们都为Android开发人员提供了一些便利的工具和功能。

1. "kotlin-android" 插件： 这是在Android项目中使用Kotlin语言的必要插件。它包含了一些在Android Studio IDE中进行Kotlin开发必要的特性，比如Kotlin代码文件的处理，与安卓SDK的交互等。如果移除了这个插件，那么你将不能在你的Android应用项目中使用Kotlin。

2. "kotlin-android-extensions" 插件： 这个插件扩展了当初"Kotlin-android"的功能，提供了额外的功能如视图绑定等。之前，开发人员经常利用这个插件通过ID直接访问视图，无需 `findViewById()`。然而，Google已经引入了更强大的View Binding和Data Binding，所以"kotlin-android-extensions"已经被弃用。如果你移除这个插件，也可以正常开发，你只需要替换原有的代码到新的视图绑定方式。

总的来说，这两个插件的区别在于，"kotlin-android" 是使用Kotlin语言在Android项目中进行开发的基础插件，而 "kotlin-android-extensions" 插件则提供了一些方便的扩展功能。目前，在更新的Android开发实践中，"kotlin-android-extensions" 插件已不再需要。