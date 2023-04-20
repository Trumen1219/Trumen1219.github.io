---
title: Question
date: 2023-01-01 00:00:00
tags: Question
layout: aboutQuestion
--- 

# object 的哪些属性不能被 stringfy
在 JavaScript 中，stringify 方法用于将对象转换为字符串。然而，并非所有对象属性都可以被 stringify 方法转换为字符串。以下是一些不能被 stringify 方法转换为字符串的属性:

函数属性:函数属性不能被 stringify 方法转换为字符串，因为它们不是对象属性。

循环引用属性:如果对象之间存在循环引用，则 stringify 方法将无法正确处理这些属性，因为它们会导致字符串化过程崩溃。

只读属性:对象中的只读属性不能被 stringify 方法转换为字符串，因为它们不能被修改。

内置对象属性:例如 Infinity, NaN, Date.prototype.getTime,以及 Array.prototype.join 等内置对象属性不能被 stringify 方法转换为字符串。

非 5.1 版本的 DOM 对象属性：在早期的 JavaScript 版本中，stringify 方法无法正确处理 DOM 对象属性，因为这些属性不是对象属性。
