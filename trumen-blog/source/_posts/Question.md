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

# 如何通过原型修改第三方类库，来实现自己的功能而不破坏类库？手写一下

要通过原型修改第三方类库，可以遵循以下步骤:

读取第三方类库的原型链。假设您正在修改 util.js 类库，您可以使用以下代码读取它的原型链:
``` js
const util = require('util');  
const p = require('path').resolve(__dirname, 'util.js');  
const utilPrototype = Object.getPrototypeOf(p);  
```
创建一个新的实例，该实例将继承第三方类库的原型。您可以使用以下代码创建一个新实例:
```js
const newUtil = Object.create(utilPrototype);  
```
修改新实例的原型链，以包含您需要的功能。您可以使用以下代码修改新实例的原型链:
```js
newUtil.prototype = Object.create(utilPrototype.prototype);  
```
将新实例返回给第三方类库。您可以使用以下代码将新实例返回给第三方类库:
```js
const util = require('util');  
const newUtil = Object.create(utilPrototype);  
return newUtil;  
```
通过这些步骤，可以修改第三方类库的原型链，以实现您需要的功能，而又不会破坏类库本身。请注意，这些步骤仅适用于您需要修改的类库是使用原型继承的。如果您需要修改基于类的类库，请考虑使用构造函数。