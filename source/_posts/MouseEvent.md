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