---
title: ios-project
date: 2022-01-14 14:19:00
tags:
---
## files

### project.pbxproj
- The Xcode project file is an old-style plist (Next style) based on braces大括号 to delimit the hierarchy. The file begins with an explicit encoding information, usually the UTF-8 one. 
- plist
- http://www.monobjc.net/xcode-project-file-format.html
```
Root Element
The root section contains the general informations.

Attribute	Type	Value	Comment
archiveVersion	Number	1	Default value.
classes	List	Empty	
objectVersion	Number		See XcodeCompatibilityVersion enumeration.
objects	Map	A map of element	The map is indexed by the elements identifier.
rootObject	Reference	An element reference	The object is a reference to a PBXProject element.
```

### setup
- pod install
- 安装完成后，打开生成的 .xcworkspace 文件，并使用此文件打开您的项目。不要使用原始的 .xcodeproj 文件打开项目，否则项目将无法使用新安装的依赖项
- 保证网络 or 切换稳定源（pod repo）
- 等待Indexing(Indexing 是 Xcode 中必要的过程，可以提高编码效率和编译速度。如果 Indexing 过程耗时较长或出现问题，可以尝试暂停 Indexing、清理 DerivedData 和优化代码结构等方法来解决问题)

### https://cocoapods.org/
- CocoaPods.org 是 CocoaPods 官方网站，提供了 CocoaPods 的搜索引擎、文档、指南、社区等资源。在该网站上，你可以搜索并找到符合需求的 Pods，并查看其用法、版本历史、许可证等信息。此外，CocoaPods.org 还提供了 Pod 创建、发布和管理等功能，是 CocoaPods 开发和使用的重要平台。

- CocoaControls 则是一个第三方网站，主要提供了 iOS 和 macOS 开发中常用的 UI 控件和库。在该网站上，你可以浏览并下载各种开源 UI 组件，如按钮、标签、表格、图表、动画等。这些组件大多数都是基于 CocoaPods 库构建的，因此你可以在 CocoaControls 网站上直接查看并复制 Podfile 中的代码，以便更轻松地集成到项目中。

- podfile - ruby
- do|end

### SwiftPM


### spec repo trunk
- pod trunk
- pod trunk register EMAIL 'NAME' --description='DESCRIPTION'
- pod trunk push PODSPEC_FILE

### podfile
- "use_frameworks!" 是一个在使用 CocoaPods 管理 iOS 项目依赖库时，用于指定是否使用动态框架的命令。

- 当在 Podfile 中添加 "use_frameworks!" 后，在安装依赖库时，CocoaPods 将会通过生成并链接动态框架的方式来管理项目中的第三方库。这种方式相对于静态库链接的方式可以减小最终 App 的大小，并且能够更好地管理依赖性。
- 需要注意的是，如果项目依赖库中有一些只提供了静态库而没有提供动态库的话，使用 "use_frameworks!" 可能会导致编译错误。此时可以考虑手动将这些库作为静态库集成到项目中，或者使用其他的依赖管理工具来处理这种情况。
```
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ''
            config.build_settings['CODE_SIGNING_REQUIRED'] = 'NO'
            config.build_settings['CODE_SIGNING_ALLOWED'] = 'NO'
        end
    end
end
```
- 在使用 CocoaPods 管理 iOS 项目依赖库时，为所有的 Pod 库设置编译选项以关闭代码签名功能。代码签名是一种苹果公司用于保护 App 安全性和防止恶意软件入侵的机制，但有时在开发过程中可能会因为证书问题或其他原因导致编译失败。
- 该代码将 EXPANDED_CODE_SIGN_IDENTITY、CODE_SIGNING_REQUIRED 和 CODE_SIGNING_ALLOWED 这三个选项都设置为 NO，这样就可以禁用代码签名功能了。需要注意的是，这种做法通常只适用于开发和测试环境，发布到 App Store 前仍然需要进行正式的代码签名和验证。
```
  pod 'DoraemonKit/Core', '~> 3.0.4', :configurations => ['Release_Test']
```
- 引用的是 DoraemonKit/Core 库的 3.0.4 版本，并且只有当当前项目的配置为 Release_Test 时才会包含该库。这意味着该库仅在 Release_Test 配置下才会被引入，并且在其他配置下不会被包含在项目中。
- DoraemonKit 是一款 iOS 开发者调试工具集合，包含了多个实用工具，如性能检测、UI 展示、网络拦截等。Core 模块是 DoraemonKit 的核心库之一，包含了基础的工具和框架，可以帮助开发者快速构建和扩展更加强大的调试工具。
### https://bugly.qq.com/
- https://bugly.qq.com/docs/user-guide/instruction-manual-ios/?v=1.0.0

### bonree


### 卡顿分析
- "NotSmoothFrameException" 这个问题在 iOS 应用程序中通常被称为卡顿（Jank），它可能会导致应用程序响应变慢，用户体验下降。

### 错误分析
- # SIGKILL The application did not terminate cleanly but no crash occured.
- 这个消息提示，意味着应用程序在运行过程中被强制终止了。SIGKILL 是一种 Unix 信号，用于强制终止进程，因此这种情况可能是由系统或用户手动杀死了进程导致的。
- 与 SIGKILL 不同的是，如果应用程序崩溃了，会触发 SIGSEGV 或 SIGBUS 信号，Crash 报告工具（如 Crashlytics 或 Bugly）通常可以捕获这些信号并生成相应的报告。但是，在没有崩溃的情况下，一些监控工具可能会记录 SIGKILL 信号以帮助开发人员进行故障排除，获取更多关于应用程序运行时的上下文信息。


### 崩溃分析
- 


#### exportoptions.plist 
是 Xcode 中用于导出 iOS 应用程序的配置文件，它包含了一些指定导出选项和目标设备信息的属性。

当开发者需要将自己的应用程序发布到 App Store 或者分发到其他用户时，可以使用 Xcode 的 Export 功能来生成一个可安装的 IPA 文件。在执行 Export 操作之前，需要先选择一些导出选项，如导出方式（Ad Hoc、App Store 等）、目标设备、证书等，并将这些选项保存为 exportoptions.plist 配置文件。

exportoptions.plist 文件是一个 XML 格式的文本文件，其中包含了多个键值对，每个键表示一个导出选项，对应的值表示该选项的设置。例如，"method" 键表示导出方式，可以设置为 "app-store"、"ad-hoc" 等；"teamID" 键表示开发者团队的唯一标识符，用于验证证书等信息。

#### release_achive_pre_action.sh
是指在 Xcode 中进行 Archive（归档）操作前自定义执行的脚本或命令。

在 Xcode 中，Archive 操作是将项目打包成一个可发布的 IPA 文件的过程。在执行该操作之前，有时需要执行一些额外的操作，例如版本号更新、代码检查等。这时就可以使用 "release_achive_pre_action" 这个钩子来实现这些自定义任务。

要配置 "release_achive_pre_action"，可以在项目的 Build Phases 设置中选择 "Editor" > "Add Build Phase" > "Add Run Script Build Phase"，然后在脚本编辑器中编写需要执行的脚本或命令即可。在执行 Archive 操作时，Xcode 将会先执行设置的所有 pre-action 内容，再执行 Archive 操作本身。

#### "build_test.sh" 是一个 shell 脚本，用于在 Xcode 中自定义构建测试的过程。

在 iOS 应用程序开发中，我们通常需要编写一些单元测试和集成测试来保障代码的质量和稳定性。Xcode 提供了对 XCTest 框架的支持，可以很方便地进行测试。但是，有时开发者可能需要执行一些额外的操作或者使用其他的测试框架来进行测试，这时就可以使用 "build_test.sh" 这个脚本来自定义测试构建流程。

"build_test.sh" 脚本可以包含一些特殊的命令，例如 xcodebuild 和 xctool 等，用于编译测试包、运行测试并将测试结果输出到指定位置。通过编写自定义的 "build_test.sh" 脚本，开发者可以更灵活地管理项目的测试流程，并满足不同的测试需求。

#### info.plist 是 iOS 应用程序中的一个属性列表文件，包含了应用程序的基本信息和配置参数。

在 info.plist 文件中，可以定义一些键值对来指定应用程序的名称、版本号、图标、权限、URL schemes 等信息。这些信息将被系统用于显示应用程序的基本信息以及确定应用程序在设备上的行为。

例如，"CFBundleDisplayName" 键用于指定应用程序在设备上显示的名称；"CFBundleVersion" 键用于指定应用程序的版本号；"NSCameraUsageDescription" 键用于指定应用程序访问相机权限时的提示文案等。通过修改 info.plist 文件，开发者可以轻松地修改应用程序的基本信息，并调整其行为和功能。

需要注意的是，info.plist 文件是必须存在的，并且必须包含一些必要的键值对，否则应用程序将无法正常运行。

#### bridging-header.h
Use this file to import your target's public headers that you would like to expose to Swift.
"bridging-header.h" 是在使用 Swift 语言开发 iOS 应用程序时，将 Objective-C 代码引入到 Swift 项目中的一种方式。

由于 Swift 和 Objective-C 是两种不同的编程语言，它们之间并不完全兼容，因此在进行混合编程时需要进行桥接。在 Xcode 中，可以创建一个名为 "bridging-header.h" 的文件，并在其中包含需要引入的 Objective-C 头文件。这样，Swift 代码就可以访问并使用 Objective-C 类和方法了。

要使用 bridging-header.h 文件，需要先在 Build Settings 中设置 "Objective-C Bridging Header" 选项，将其设置为 bridging-header.h 文件的路径。然后，在 Swift 代码中就可以通过 import 关键字来引入 Objective-C 类和方法，从而实现混合编程的目的。

需要注意的是，虽然可以通过 bridging-header.h 文件将 Objective-C 代码引入到 Swift 项目中，但是反过来却不行。也就是说，Objective-C 项目无法直接引入 Swift 代码，需要通过其他方式实现混合编程。


#### "AppDelegate.swift" 是在使用 Swift 语言开发 iOS 应用程序时，应用程序的入口文件和主要配置文件。

在 AppDelegate.swift 文件中，包含了应用程序启动时需要执行的代码和各种配置选项。例如，在该文件中可以定义应用程序的窗口、根视图控制器、推送通知设置、URL schemes 处理等功能。同时，AppDelegate.swift 还提供了多个生命周期方法，如 application(:didFinishLaunchingWithOptions:)、applicationDidBecomeActive(:) 等，用于处理应用程序在不同状态下的行为和逻辑。

需要注意的是，虽然 AppDelegate.swift 是应用程序的主要入口文件，但它并不是唯一的入口点。在应用程序中，还可以通过 SceneDelegate.swift 文件（仅适用于 iOS 13 及以上版本）和 SwiftUI 的 @main 注解来定义应用程序的入口点。
NS的全称是NextStep，它是苹果公司早期开发的一种面向对象编程框架，现在被整合到了Cocoa和Cocoa Touch中。NSLocalizedString函数是一个用于本地化字符串的Objective-C语言中的宏，它可以帮助开发者根据用户的语言环境来获取相应的翻译字符串。

"zh-hans.lproj"是一个语言环境标识符，表示简体中文。在iOS和macOS开发中，开发者可以通过在工程项目中添加不同语言环境的本地化文件夹，并在其中放置对应语言的本地化字符串文件来实现多语言支持。其中，".lproj"是"language project"（语言项目）的缩写。

"launchScreen.strings"是一个字符串文件的文件名，它通常用于应用程序启动画面的本地化。这个文件包含了用于展示启动画面的字符串，可以根据用户的语言环境进行本地化翻译。在该文件中，开发者可以使用NSLocalizedString函数来获取本地化字符串。

#### "Base.lproj"是一个语言环境标识符，表示基础语言环境。在iOS和macOS开发中，开发者可以通过在工程项目中添加不同语言环境的本地化文件夹，并在其中放置对应语言的本地化字符串文件来实现多语言支持。

"Base.lproj"文件夹通常包含项目中默认的本地化字符串文件，这些字符串将作为其他语言版本的备选项。如果应用程序在运行时无法找到特定语言的本地化字符串，系统将会回退并使用"Base.lproj"文件夹中的字符串作为默认值。因此，开发者需要确保"Base.lproj"文件夹中包含了所有必要的本地化字符串，并且这些字符串能够清晰、准确地表达应用程序的功能和信息。

"launchScreen.storyboard"是一个故事板文件的文件名，它通常用于应用程序启动画面的设计。在iOS和macOS开发中，启动画面是应用程序第一次启动时显示给用户的界面，通常用来展示应用程序的品牌、公司或者产品信息。

与传统的XIB文件不同，故事板（Storyboard）是一种更加高级的用户界面设计工具，可以在其中同时包含多个页面的设计，以及这些页面之间的流程和跳转关系。在故事板中设计完成后，可以使用代码来加载和控制这些页面，并将其作为应用程序的一部分进行发布。

#### assets.xcassets
在iOS和macOS开发中，图像资源是应用程序界面设计的重要组成部分。为了方便管理这些资源，开发者可以将它们放置在"assets.xcassets"文件夹中，并使用Xcode的图形化界面来进行预览、编辑和设置属性。其中，".xcassets"是“Xcode Assets”的缩写，表示这个文件夹是由Xcode管理的资源库。同时，该文件夹还支持不同屏幕尺寸和设备类型之间的自动适配，使得应用程序更加灵活和易于维护。