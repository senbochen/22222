---
title: JavaScript 的三座大山
index_img: /img/1.jpg
date: 2023-1-11 12:04:00
sticky: 100
---

### 1️⃣ 作用域

作用域 指代码当前上下文，控制着变量和函数的可见性和生命周期。最大的作用是隔离变量，不同作用域下同名变量不会冲突。
作用域链 指如果在当前作用域中没有查到值，就会向上级作用域查询，直到全局作用域，这样一个查找过程所形成的链条就被称之为作用域链。
作用域可以堆叠成层次结构，子作用域可以访问父作用域，反之则不行。
作用域具体可细分为四种：全局作用域、模块作用域、函数作用域、块级作用域
全局作用域： 代码在程序的任何地方都能被访问，例如 window 对象。但全局变量会污染全局命名空间，容易引起命名冲突。
模块作用域： 早期 js 语法中没有模块的定义，因为最初的脚本小而简单。后来随着脚本越来越复杂，就出现了模块化方案（AMD、CommonJS、UMD、ES6 模块等）。通常一个模块就是一个文件或者一段脚本，而这个模块拥有自己独立的作用域。
函数作用域： 顾名思义由函数创建的作用域。闭包就是在该作用域下产生，后面我们会单独介绍。
块级作用域： 由于 js 变量提升存在变量覆盖、变量污染等设计缺陷，所以 ES6 引入了块级作用域关键字来解决这些问题。典型的案例就是 let 的 for 循环和 var 的 for 循环。

```
// var demo
for(var i=0; i<10; i++) {
console.log(i);
}
console.log(i); // 10

// let demo
for(let i=0; i<10; i++) {
console.log(i);
}
console.log(i); //ReferenceError：i is not defined

```

---

## 2️⃣ 原型和原型链

---

有对象的地方就有 原型，每个对象都会在其内部初始化一个属性，就是 prototype(原型)，原型中存储共享的属性和方法。当我们访问一个对象的属性时，js 引擎会先看当前对象中是否有这个属性，如果没有的就会查找他的 prototype 对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。这么一个寻找的过程就形成了 原型链 的概念。
理解原型最关键的是理清楚**proto**、prototype、constructor 三者的关系，我们先看看几个概念：

- **proto**属性在所有对象中都存在，指向其构造函数的 prototype 对象；prototype 对象只存在（构造）函数中，用于存储共享属性和方法；constructor 属性只存在于（构造）函数的 prototype 中，指向（构造）函数本身。
- 一个对象或者构造函数中的隐式原型**proto**的属性值指向其构造函数的显式原型 prototype 属性值，关系表示为：instance.**proto** === instance.constructor.prototype
- 除了 Object，所有对象或构造函数的 prototype 均继承自 Object.prototype，原型链的顶层指向 null：Object.prototype.**proto** === null
- Object.prototype 中也有 constructor：Object.prototype.constructor === Object
- 构造函数创建的对象（Object、Function、Array、普通对象等）都是 Function 的实例，它们的 **proto** 均指向 Function.prototype。

```
const arr = [1, 2, 3];
arr.__proto__ === Array.prototype; // true
arr.__proto__.__proto__ === Object.prototype; // true
Array.__proto__ === Function.prototype; // true
```

---

## 3️⃣ 异步和单线程

---

JavaScript 是 单线程 语言，意味着只有单独的一个调用栈，同一时间只能处理一个任务或一段代码。队列、堆、栈、事件循环构成了 js 的并发模型，事件循环 是 JavaScript 的执行机制。

为什么 js 是一门单线程语言呢？最初设计 JS 是用来在浏览器验证表单以及操控 DOM 元素，为了避免同一时间对同一个 DOM 元素进行操作从而导致不可预知的问题，JavaScript 从一诞生就是单线程。

既然是单线程也就意味着不存在异步，只能自上而下执行，如果代码阻塞只能一直等下去，这样导致很差的用户体验，所以事件循环的出现让 js 拥有异步的能力。

![事件循环](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7bdd4419989d4bec8ac627480572cf84~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

---

### 听一首妈妈的话

[妈妈的话](https://www.bilibili.com/video/BV1fa411X7dK/?spm_id_from=333.337.search-card.all.click&vd_source=639516599ed6bf817b6a6c8eb26fb2eb)
