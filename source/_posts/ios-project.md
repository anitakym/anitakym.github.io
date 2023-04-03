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