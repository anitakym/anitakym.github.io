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