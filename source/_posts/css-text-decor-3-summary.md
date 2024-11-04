---
title: css-text-decor-3-summary
date: 2024-02-23 14:25:18
tags:
---
https://www.w3.org/TR/css-text-decor-3/#line-decoration

## CSS Text Decoration Level 3 概述

在现代网页设计中，文本装饰是一个重要的视觉元素。CSS Text Decoration Level 3 规范（[CSS Text Decoration Level 3](https://www.w3.org/TR/css-text-decor-3/#line-decoration)）为开发者提供了更多的控制和灵活性，以便更好地装饰文本。本文将介绍该规范中的一些关键特性和用法。

### 1. 文本装饰线

CSS Text Decoration Level 3 规范引入了对文本装饰线（text decoration lines）的更细粒度控制。以下是一些常用的属性：

- [`text-decoration-line`]: 指定文本装饰线的类型，如 `underline`（下划线）、`overline`（上划线）和 [`line-through`]（删除线）。
- [`text-decoration-style`]: 指定装饰线的样式，如 `solid`（实线）、`double`（双线）、`dotted`（点线）、`dashed`（虚线）和 `wavy`（波浪线）。
- [`text-decoration-color`]: 指定装饰线的颜色。

示例代码：
```css
p {
  text-decoration-line: underline;
  text-decoration-style: wavy;
  text-decoration-color: red;
}
```

### 2. 文本装饰的简写属性

为了简化代码，CSS 提供了一个简写属性 [`text-decoration`]，可以同时设置装饰线的类型、样式和颜色。

示例代码：
```css
p {
  text-decoration: underline wavy red;
}
```

### 3. 文本装饰的间距

[`text-decoration-skip-ink`]属性允许开发者控制装饰线是否跳过文本中的墨水部分，以提高可读性。该属性的值可以是 `auto` 或 `none`。

示例代码：
```css
p {
  text-decoration-skip-ink: auto;
}
```

### 4. 文本装饰的厚度

[`text-decoration-thickness`]属性允许开发者指定装饰线的厚度。可以使用绝对值（如 `2px`）或相对值（如 `from-font`）。

示例代码：
```css
p {
  text-decoration-thickness: 2px;
}
```

### 5. 文本装饰的继承性

CSS Text Decoration Level 3 规范还定义了文本装饰的继承行为。默认情况下，文本装饰是继承的，但可以通过设置 [`text-decoration`]属性来覆盖继承的值。

示例代码：
```css
.parent {
  text-decoration: underline;
}

.child {
  text-decoration: none;
}
```

### 结论

CSS Text Decoration Level 3 规范为开发者提供了更强大的工具来控制文本装饰。通过使用这些新特性，开发者可以创建更加美观和可读的网页内容。希望本文能帮助你更好地理解和应用这些新特性。

更多详细信息，请参考 [CSS Text Decoration Level 3 规范](https://www.w3.org/TR/css-text-decor-3/#line-decoration)。