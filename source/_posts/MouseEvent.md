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
