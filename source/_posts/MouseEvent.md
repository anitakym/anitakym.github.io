---
title: MouseEvent
date: 2020-03-07 09:56:56
tags: 
    - Event
---
> 鼠标事件（The MouseEvent interface represents events that occur due to the user interacting with a pointing device (such as a mouse).）

* MDN指路：https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent

MouseEvent 包括
- click
- dblclick
- mouseup
- mousedown

MouseEvent derives from UIEvent 
UIEvent derives from Event

一些具体的事件都派生自 MouseEvent：WheelEvent 和DragEvent。

Properties
This interface also inherits properties of its parents, UIEvent and Event.

其中：
- MouseEvent.clientX Read only
The X coordinate of the mouse pointer in local (DOM content) coordinates.
- MouseEvent.clientY Read only
The Y coordinate of the mouse pointer in local (DOM content) coordinates.
- MouseEvent.offsetX Read only
The X coordinate of the mouse pointer relative to the position of the padding edge of the target node.
- MouseEvent.offsetY Read only
The Y coordinate of the mouse pointer relative to the position of the padding edge of the target node.
- MouseEvent.pageX Read only
The X coordinate of the mouse pointer relative to the whole document.
- MouseEvent.pageY Read only
The Y coordinate of the mouse pointer relative to the whole document.
- MouseEvent.screenX Read only
The X coordinate of the mouse pointer in global (screen) coordinates.
- MouseEvent.screenY Read only
The Y coordinate of the mouse pointer in global (screen) coordinates.

#### concept
 screenX/screenY：相对屏幕区域左上角定位，若发生滚动行为，则相对该区域定位
 pageX/pageY：相对网页区域左上角定位
 clientX/clientY：相对浏览器可视区域左上角定位
 offsetX/offsetY：相对父节点区域左上角定位，若无父节点则相对<html>或<body>定位

## KeyboardEvent
- https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent
- 键盘事件是由焦点系统控制的，一般来说，操作系统也会提供一套焦点系统，但是现代浏览器一般都选择在自己的系统内覆盖原本的焦点系统
- 焦点系统认为整个 UI 系统中，有且仅有一个“聚焦”的元素，所有的键盘事件的目标元素都是这个聚焦元素
- 浏览器也提供的API来处理焦点，focus,blur
- 键盘事件为了跟 pointer 设备保持一致，也规定了从外向内传播的捕获过程
```
Note: KeyboardEvent events just indicate what interaction the user had with a key on the keyboard at a low level, providing no contextual meaning to that interaction. When you need to handle text input, use the input event instead. Keyboard events may not be fired if the user is using an alternate means of entering text, such as a handwriting system on a tablet or graphics tablet.
```
- key | code    keyCode ()

## FocusEvent
- https://developer.mozilla.org/en-US/docs/Web/API/FocusEvent
- https://javascript.info/focus-blur
- https://w3c.github.io/uievents/#events-focusevent-doc-focus


https://caniuse.com/?search=pointer-events
CSS pointer-events (for HTML)  - UNOFF
This CSS property, when set to "none" allows elements to not receive hover/click events, instead the event will occur on anything behind it.
当此 CSS 属性设置为“none”时，允许元素不接收悬停/单击事件，而是该事件将发生在其后面的任何内容上。

Pointer events  - REC
This specification integrates various inputs from mice, touchscreens, and pens, making separate implementations no longer necessary and authoring for cross-device pointers easier. Not to be mistaken with the unrelated "pointer-events" CSS property.
该规范集成了来自鼠标、触摸屏和笔的各种输入，使不再需要单独的实现，并且更容易为跨设备指针进行创作。不要与不相关的“指针事件”CSS 属性混淆。