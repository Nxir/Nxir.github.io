---
title: JS运行原理
tags:
    - Web前端
    - JavaScript
---

## JS 动态类型的特性

动态类型语言在编码时提供的信息太少了,让编译器无法在运行前知道变量的类型,只有在运行期间才能确定各个变量的类型,这就导致 JS 无法在运行前编译出更加快速的低级语言的代码,也就是机器代码(Machine Code)

<!-- more -->

## 事件循环 & 异步回调

JavaScript 的执行环节是一个单线程,也就意味着 JS 环境只有一个调用栈,如果调用栈中某个函数执行需要消耗大量时间,就会导致调用栈被阻塞,无法入栈和出栈

由于浏览器中页面的布局绘制和 JS 的执行是共用的同一个主线程,如果 JS 的处理迟迟不归还主线程的话,就会影响页面的渲染,导致页面卡顿

优化的方法就是使用事件循环 & 异步回调

{% note no-icon %}
[What the heck is the event loop anyway? ](https://www.youtube.com/watch?v=8aGhZQkoFbQ&t=3s)

[一文带你搞懂 JavaScript 事件循环](https://juejin.im/post/6844903881663578119)
{% endnote %}

## JIT & AOT

Just In Time(JIT)在运行时生成机器代码,而不是提前生成.在运行阶段收集类型信息,然后根据信息编译机器码,之后再运行代码时直接使用机器码

Ahead Of Time(AOT)在运行前提前生成好机器码

## JavaScript 引擎

1.  引擎负责将高级语言 JS 转为低级语言机器码

2.  JS 引擎首先将 JS 源码通过 parser(解析器)解析成抽象语法树(AST)

3.  接着通过 interpreter(解释器)将 AST 编译成字节码(bytecode)

4.  字节码通过 compiler(编译器)生成 machine code(机器码)

{% note  no-icon %}

字节码:是一种中间状态(中间码)的二进制代码(文件),这也是为什么 Java 这种语言可以跨平台的原因

机器码:是电脑 CPU 直接读取运行的机器指令,运行速度最快

不同平台的机器代码会有差异,所以编译器会根据当前平台(如 ARM x64)编译出不同平台的机器码,这里的机器码其实就是汇编代码

{% endnote %}

#### 参考

[📹 JS 运行原理](https://www.bilibili.com/video/BV1vh411Z7QG)
[📹 V8 引擎如何运行](https://www.bilibili.com/video/BV1zV411z7RX)
[📹 JS 调用栈](https://www.bilibili.com/video/BV13k4y1y7vU)
