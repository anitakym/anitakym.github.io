---
title: app-软键盘
date: 2024-03-18 14:40:02
tags:
---
在应用开发中，调用软键盘通常与输入框相关。当用户需要输入某些信息时，应用程序需要调用软键盘供用户输入。下面是如何在Android和iOS应用中调用软键盘：

1. Android：

在Android中，通常我们不需要显式调用软键盘，只需要设置EditText获取焦点即可。如果确实需要显式调用，可以使用InputMethodManager类来做到。

如下面的示例代码：

```java
//获取InputMethodManager的实例
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE); 
//请求显示软键盘
imm.showSoftInput(editText, InputMethodManager.SHOW_IMPLICIT);
```
同样的，如果需要显式关闭软键盘，可以使用hideSoftInputFromWindow函数：
   
```java
//获取当前焦点的View
View currentFocusView = getCurrentFocus();
//请求隐藏软键盘
if (currentFocusView != null) {
      imm.hideSoftInputFromWindow(currentFocusView.getWindowToken(), 0);
}
```

2. iOS：

在iOS中，若要调用软键盘，也是以UIKit中的输入控件(UITextField, UITextView)获取焦点为主。可以通过将resignFirstResponder设为false来请求键盘出现，设为true来使键盘消失。

调用软键盘的代码如下：
   
```swift
// 请求键盘
textField.becomeFirstResponder()
```
   
隐藏软键盘的代码如下：

```swift
// 隐藏键盘
textField.resignFirstResponder()
```

需要注意的是，某些情况下，我们还需要根据实际业务需求，实现键盘的相关操作，比如在键盘上添加完成按钮或自定义工具栏等。

在 Android 系统中，可以通过创建一个输入法服务以定制系统软键盘。以下是创建输入法服务的大致步骤：

1. 创建一个 Java 类，该类需要继承自 `InputMethodService`。`InputMethodService` 是 Android 提供的用于创建自定义输入法服务的基类。

    ```java
    public class MyInputMethodService extends InputMethodService {
        ...
    }
    ```

2. 在这个类中，你需要覆盖并实现以下两个方法：
     - `onCreateInputView()`：此方法用于创建键盘的视图。
     - `onCreateInputMethodInterface()`：此方法用于创建你的输入法的接口。

   例如：
    
    ```java
    public class MyInputMethodService extends InputMethodService {

        @Override
        public View onCreateInputView() {
            // 创建并加载键盘视图  
            View keyboardView = getLayoutInflater().inflate(R.layout.keyboard, null);
            return keyboardView;
        }

        @Override
        public AbstractInputMethodService.AbstractInputMethodImpl onCreateInputMethodInterface() {
            // 创建并加载键盘的接口
            return super.onCreateInputMethodInterface();
        }
    }
    ```

3. 在你的 AndroidManifest.xml 文件中，你需要注册你的输入法服务。

    ```xml
    <service
        android:name=".MyInputMethodService"
        android:label="@string/service_name"
        android:permission="android.permission.BIND_INPUT_METHOD">
        <intent-filter>
            <action android:name="android.view.InputMethod" />
        </intent-filter>
        <meta-data
            android:name="android.view.im"
            android:resource="@xml/method" />
    </service>
    ```

一旦键盘服务创建并启动，用户就可以在设置->语言和输入法->输入法列表中找到你的键盘并进行切换。定制软键盘的布局、功能等都在你创建的键盘服务的类中进行。

在iOS中，你无法直接定制系统的软键盘，这主要是出于安全和隐私的原因。然而，你可以开发一个键盘应用来提供自定义的输入体验，这是被允许的。这被称为“键盘扩展”。

以下是创建自定义键盘的基本步骤：

1. 在 Xcode 中，创建一个新的 "Keyboard Extension"。你可以选择 "File" > "New" > "Target"，然后从 "Application Extension" 类别找到 "Custom Keyboard Extension"。

2. 这样，你就成功创建了一个新的键盘扩展。其中的 "KeyboardViewController.swift" 文件是你需要重点关注的，它负责键盘的展示和用户交互。

3. 你可以在 "KeyboardViewController.swift" 文件中重写几个主要方法来实现你自己的键盘布局和逻辑，例如：`updateViewConstraints`，`viewDidLoad` 和 `textWillChange` 等。

需要注意的是，自定义键盘扩展涉及到许多隐私问题，因为键盘能够获知用户所输入的所有内容。出于隐私考虑，iOS 对键盘扩展施加了很多限制，例如无法访问到用户的摄像头、相册等资源，也无法调用网络服务。

使用自定义键盘扩展，你可以实现一些优化输入体验的功能，如自定义键盘布局、添加表情键等。

### 
如果你要创建一个自定义键盘并且能在键盘中进行输入，你需要利用iOS在App Extensions（应用扩展）中所提供的Custom Keyboard Extension（自定义键盘扩展）。然后在键盘扩展中处理键盘的输入。

下面是实现这一功能的基本步骤：

1. 创建键盘扩展：打开Xcode，点击 "File" > "New" > "Target"，然后选择 "Application Extension" > "Custom Keyboard Extension"。

2. 实现键盘输入：在你的自定义键盘扩展中，核心的类是UIInputViewController。UIInputViewController类负责接收和处理用户的输入。你需要创建一个扩展了UIInputViewController的类，并且重写它的输入方法。

中文字母输入可以通过`self.textDocumentProxy`提供的`adjustTextPosition(byCharacterOffset:)`和`insertText(_:)`方法来实现。例如，当用户按下一个键时，你可以调用`insertText(_:)`方法将该键对应的文字插入到文本中。

```swift
let proxy = self.textDocumentProxy as UITextDocumentProxy
proxy.insertText("你的文字")
```

3. 创建键盘界面：你可以利用Interface Builder来设计键盘的界面，或者在代码中创建。界面可以包含多个UIButton，当按钮被按下时，对应的文字通过上一步的方式输入到文本中。

记得，在info.plist文件中将RequestsOpenAccess设为YES，这样键盘扩展就可以访问全键盘输入。

以上就是基础的实现方式，你还可以通过添加更多的交互和动画，来丰富你的键盘应用。

定义方式可能会因具体需求和应用的独特性而有所不同，我建议查阅Apple开发者文档中关于Custom Keyboard的部分来获取更详细的信息。


https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/CustomKeyboard.html


### 参考文章
- https://juejin.cn/post/6961757804491178014?searchId=20240314170238D0A68EC648BFF98B340D

https://setcina.github.io/2020/01/20/WebView%E4%B8%8A%E8%BD%AF%E9%94%AE%E7%9B%98%E7%9A%84%E5%85%BC%E5%AE%B9%E6%96%B9%E6%A1%88/

WebView上软键盘的兼容方案

https://juejin.cn/post/6844904199474397191?searchId=20240314170238D0A68EC648BFF98B340D（WKWebView支持代码focus唤起键盘）