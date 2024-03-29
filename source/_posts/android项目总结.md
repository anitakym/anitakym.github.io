---
title: android项目总结
date: 2021-11-01 16:14:13
tags:
---

## 环境配置

### doc
- https://developer.android.com/studio/releases/platforms#9.0
### Error 
#### Gradle sync failed: Could not install Gradle distribution from 'https://services.gradle.org/distributions/gradle-6.7.1-all.zip'. (40 s 221 ms)
- ping了下这个域名 -> ping: cannot resolve https://services.gradle.org/distributions/gradle-6.7.1-all.zip: Unknown host
- Gradle Scripts ->  gradle-wrapper.properties -> 在官网找到对应版本，下载，把能下载的地址粘贴过来(https\://downloads.gradle-dn.com/distributions/gradle-6.7.1-all.zip) 
- https://developer.android.com/studio/build/?hl=zh-cn , Gradle官方相关配置说明

#### Could not resolve all dependencies for configuration ':classpath'.
- Using insecure protocols with repositories, without explicit opt-in, is unsupported.
- http 改成 https
### build err
build => rebuild




## WebView
x5内核	原生webview
内核版本	统一Blink内核(基于chromium)	4.4以下WebKit，4.4以上chromium

### 调试
- https://github.com/google/ios-webkit-debug-proxy
## Code-Review-Fix
### 闪黑屏
```
public abstract class BaseAppCompatActivity extends AppCompatActivity {
    @Override
    protected void onPause() {
        super.onPause(); //fix
        if (!isXXX()) {
            return;
        }
        // origin 
        // super.onPause(); 
    }
}
```
Web调用原生提供的openPage的方法，中间会闪黑屏，Android的查问题，发现这个问题；

## 单位
- dp：Density-independent pixels
- 以160PPI屏幕为标准，则1dp=1px
- dp*ppi/160 = px
- sp：Scale-independent pixels
- 以160PPI屏幕为标准，当字体大小为 100%时， 1sp=1px
- sp*ppi/160 = px
- 建议文字用sp单位，非文字用dp单位
- dp,sp 让物理感官上面的高度呈现不会因为设备的分辨率而受影响
```
 <TextView
            android:id="@+id/tv_content"
            style="@style/widget_font_medium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:paddingHorizontal="8dp"
            android:text="@string/home_ai_speech_tip"
            android:textColor="@color/widget_color_white"
            android:textSize="16sp"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

```
## 混淆
- build process
## 加固
- apk文件
- 爱加密移动APP安全加固系统
- https://www.ijiami.cn/AppProtect/
### 问题处理
- .so , https://developer.android.com/ndk/guides/abis?hl=zh-cn
- 加固之后，之前处理webview的包，需要再加个插件，解决加固之后的问题
- 如果有注解的包，可能在加固之后容易有问题，需要做好处理

### activity - launchmode - singletask
android:launchMode="singleTask"
停机维护页面,和服务端约定接口状态，给出弹窗
改成singleTask，类似于web的单例模式，这样只有唯一一个弹框了

### user-agent 大赏
#### 小米平板
- Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/89.0.4389.116 Safari/534.24 Device/nabu Model/21051182C XiaoMi/MiuiBrowser/14.6.62

### 屏幕分辨率问题
- 锁放大缩小

### android端部分机型口语评测无法使用
- 反馈情况为，第一次能用，后面突然无法使用
- 同时接入了某飞的SDK（需要麦克风-语音助手类似）
- 接入了第三方口语测评SDK
- 第三方口语测评部分机型无法使用
- 真机复现 -> 发现第三方口语测评SDK调用时报错，查出受另一SDK影响，因为都需要收音的资源，麦克风被占用了，所以上报的录音结果多次为0
- 但是第三方口语测评SDK没有报错


### bugly
- Javascript的异常捕获功能
- https://bugly.qq.com/docs/user-guide/advance-features-android/?v=1.0.0#javascript


###
Hilt是一种非常好的依赖注入框架，如果按照最佳实践使用，可以大大提高Android应用的开发效率。下面是一些经验：

1. **尽可能的使用预定义的注解范围：**Hilt提供了@Singleton, @ActivityRetainedScoped, @ActivityScoped, @FragmentScoped, @ViewScoped, @ViewModelScoped 这些预定义的注解范围。尽量使用这些来标记你的依赖。

2. **在AndroidEntryPoint之下的组件中，不要使用自定义的组件依赖：**自定义的组件（使用`@DefineComponent`标注的）在`@AndroidEntryPoint`标注的类中不能保证正确的行为。

3. **仅在必要的情况下使用自定义的组件：**自定义的组件可能会让Hilt的使用变的复杂。

4. **模块中的重要标注：**对于模块中提供依赖的方法，要确保使用了`@Provides` 或 `@Binds` 标注。同时还要确保模块用`@InstallIn` 标定安装到了合适的组件中。

5. **在模块中避免使用运行时参数：**尽量避免在`@Provides`或者`@Binds` 的方法中使用运行时参数。因为Hilt得知如何提供这些参数会很困难。

6. **避免在应用启动时执行长耗时的操作：**尽量减少`@EntryPoint`或者`@Inject`在`Application`子类中执行耗时的操作，因为这会影响应用的启动时间。

7. **使用Hilt的Android测试库进行单元测试：**Hilt 提供了一套工具，用以测试使用Hilt的Android应用。

