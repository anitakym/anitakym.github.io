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
