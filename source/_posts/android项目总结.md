---
title: android项目总结
date: 2021-11-01 16:14:13
tags:
---

## 环境配置
### Error 
#### Gradle sync failed: Could not install Gradle distribution from 'https://services.gradle.org/distributions/gradle-6.7.1-all.zip'. (40 s 221 ms)
- ping了下这个域名 -> ping: cannot resolve https://services.gradle.org/distributions/gradle-6.7.1-all.zip: Unknown host
- Gradle Scripts ->  gradle-wrapper.properties -> 在官网找到对应版本，下载，把能下载的地址粘贴过来(https\://downloads.gradle-dn.com/distributions/gradle-6.7.1-all.zip) 
- https://developer.android.com/studio/build/?hl=zh-cn , Gradle官方相关配置说明

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