---
title: 学习笔记 - Vue3
tags:
    - Vue3
    - Web前端
---

{% cq %} Vue3 新特性! 就很棒! {% endcq %}

<!-- more -->

-   provide / inject
-   teleport
-   ref/reactive (两种方法都会使引用变为响应式的)
    -   ref: 由于原始类型(String,Number,Undefined,Null,Boolean)为值传递,不是引用传递,所以需要通过 ref 方法包裹原始类型,返回统一的对象属性, 通过 value 来访问
    -   reactive 展开后不再为响应式 需要使用 toRefs 方法包裹
-   watchEffect
    -   watchEffect 中有使用到的值发生变化时,watchEffect 方法将被调用
    -   可以定义多个 watchEffect 方法,分别处理不同的逻辑
    -   watchEffect 返回一个方法 调用可停止 watchEffect
-   Composition Api
    -   超大项目时使用
    -   在 setup 中定义
        -   setup 方法在组件创建前执行,所以没有 this 属性,不能访问 prop,computed,mothod (可以访问 prop, attr, slots, emit)
        -   接受参数 props 和 context
            -   props 就是 props 属性的引用
            -   context 对象暴露组件属性 context.attrs, context.emit, context.slots
                -   context 非响应式属性,所以可以使用结构写法 setup(props, { attrs, slots, emit }) { ... }
        -   setup 的返回值将暴露给组件的其他部分(计算属性,方法,声明周期,模板组件等等)
