---
title: 学习路线
date: 2020-9-11 12:00:00
type: "learning-path"
---

## 已完成

Laravel 7.0  
Laravel Valet  
Laravel Telescope  
Laravel Clockwork  
Laravel Sanctum  
Laravel Horizon  
优化 VSCODE 配置与插件  
Git Rebase 操作  
模板化 jsconfig  
CSS Grid 布局  
Less  
Vue cli  
Webpack 4  
ES 特性 Pomise Async/Await  
了解 Lodash  
复习 Vue2  
Vue 响应式原理  
Bootsrap Icons
Vue3
[使用 Hexo 搭建博客](https://www.bilibili.com/video/BV1dt4y1Q7UE)

## 正在进行

TypeScript

<details><summary>MVVM</summary>

-   VM(编译器,响应式数据,渲染器)
-   编译器(AST 抽象语法树 -> Transfer -> Generate)
    -   AST Parser 通过正则将模板字符串解析并转换为抽象语法树,即节点(JavaScript Object),包含标签名,标签属性 内容,子节点
    -   Transfer 将抽象语法树转为具象语法树(因为每个框架会有独有的标签属性,需要单独提出解析 提取,更细致的表现为在语法树中, 例如 Vue 中的指令)
    -   Generate 依据具象语法树生成渲染函数的逻辑代码

</details>

<details><summary>JS运行原理</summary>

动态类型语言在编码时提供的信息太少了,让编译器无法在运行前知道变量的类型,只有在运行期间才能确定各个变量的类型,这就导致 JS 无法在运行前编译出更加快速的低级语言的代码,也就是机器代码(Machine Code)

Just In Time(JIT)在运行时生成机器代码,而不是提前生成.在运行阶段收集类型信息,然后根据信息编译机器码,之后再运行代码时直接使用机器码

Ahead Of Time(AOT)在运行前提前生成好机器码

JavaScript 引擎(将高级语言 JS 转为低级语言机器码)

-   JS 引擎首先将 JS 源码通过 parser(解析器)解析成抽象语法树(AST)
-   接着通过 interpreter(解释器)将 AST 编译成字节码(bytecode)
-   字节码通过 compiler(编译器)生成 machine code(机器码)
    -   字节码:是一种中间状态(中间码)的二进制代码(文件),这也是为什么 Java 这种语言可以跨平台的原因
    -   机器码:是电脑 CPU 直接读取运行的机器指令,运行速度最快
    -   不同平台的机器代码会有差异,所以编译器会根据当前平台(如 ARM x64)编译出不同平台的机器码,这里的机器码其实就是汇编代码

</details>

## 计划

JavaScript Event Loop \
[数据结构](https://www.bilibili.com/video/BV1b7411N798) \
[Learngitbranching](https://learngitbranching.js.org) \
[xuesql](http://xuesql.cn/lesson/introduction) \
Sass
k8s
