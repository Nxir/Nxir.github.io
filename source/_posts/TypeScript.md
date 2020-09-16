---
title: TypeScript 笔记
tag:
    - TypeScript
    - web前端
---

{% cq %}
[一份不可多得的 TS 学习指南](https://juejin.im/post/6872111128135073806)
{% endcq %}

<!-- more -->

## 类型断言

尖括号语法

```typescript
let someValue: any = 'this is a string';
let strLength: number = (<string>someValue).length;
```

as 语法

```typescript
let someValue: any = 'this is a string';
let strLength: number = (someValue as string).length;
```

## unknown

unknown 类型只能被赋值给 any 类型和 unknown 类型本身

```typescript
let value: unknown;

let value1: unknown = value; // OK
let value2: any = value; // OK
let value3: boolean = value; // Error
let value4: number = value; // Error
let value5: string = value; // Error
let value6: object = value; // Error
let value7: any[] = value; // Error
let value8: Function = value; // Error
```

unknown 不能进行值操作

```typescript
let value: unknown;

value.foo.bar; // Error
value.trim(); // Error
value(); // Error
new value(); // Error
value[0][1]; // Error
```

## 接口 可选&只读属性

```typescript
interface Person {
    readonly name: string;
    age?: number;
}
```

只读属性用于限制只能在对象刚刚创建的时候修改其值。此外 TypeScript 还提供了 ReadonlyArray<T> 类型，它与 Array<T> 相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改。

```typescript
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
```

## 接口 任意属性

有时候我们希望一个接口中除了包含必选和可选属性之外，还允许有其他的任意属性，这时我们可以使用 索引签名 的形式来满足上述要求。

```typescript
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

const p1 = { name: 'semlinker' };
const p2 = { name: 'lolo', age: 5 };
const p3 = { name: 'kakuqo', sex: 1 };
```

## 泛型

软件工程中，我们不仅要创建一致的定义良好的 API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

泛型（Generics）是允许同一个函数接受不同类型参数的一种模板。相比于使用 any 类型，使用泛型来创建可复用的组件要更好，因为泛型会保留参数类型。

\<T>中 T 代表 Type,是一种**类型**变量,它是我们希望传递给函数的**类型占位符**

实际上 T 可以用任何有效名称代替。除了 T 之外，以下是常见泛型变量代表的意思：

-   K（Key）：表示对象中的键类型；
-   V（Value）：表示对象中的值类型；
-   E（Element）：表示元素类型。

### 泛型接口

```typescript
interface GenericIdentityFn<T> {
    (arg: T): T;
}
let f1: GenericIdentityFn<string> = (p1) => p1;
console.log(f1('Hello')); // Hello
```

### 包含泛型方法的接口

```typescript
interface IncludeGenericObj {
    fn1: <T>(v1: T) => T;
    p1?: string;
}
let f1: IncludeGenericObj = {
    fn1: (p1) => {
        return p1;
    }
};
console.log(f1.fn1(1)); // 1
```

## CompilerOptions 选项

```json
{
    "compilerOptions": {
        /* 基本选项 */
        "target": "es5", // 指定 ECMAScript 目标版本: 'ES3' (default), 'ES5', 'ES6'/'ES2015', 'ES2016', 'ES2017', or 'ESNEXT'
        "module": "commonjs", // 指定使用模块: 'commonjs', 'amd', 'system', 'umd' or 'es2015'
        "lib": [], // 指定要包含在编译中的库文件
        "allowJs": true, // 允许编译 javascript 文件
        "checkJs": true, // 报告 javascript 文件中的错误
        "jsx": "preserve", // 指定 jsx 代码的生成: 'preserve', 'react-native', or 'react'
        "declaration": true, // 生成相应的 '.d.ts' 文件
        "sourceMap": true, // 生成相应的 '.map' 文件
        "outFile": "./", // 将输出文件合并为一个文件
        "outDir": "./", // 指定输出目录
        "rootDir": "./", // 用来控制输出目录结构 --outDir.
        "removeComments": true, // 删除编译后的所有的注释
        "noEmit": true, // 不生成输出文件
        "importHelpers": true, // 从 tslib 导入辅助工具函数
        "isolatedModules": true, // 将每个文件做为单独的模块 （与 'ts.transpileModule' 类似）.

        /* 严格的类型检查选项 */
        "strict": true, // 启用所有严格类型检查选项
        "noImplicitAny": true, // 在表达式和声明上有隐含的 any类型时报错
        "strictNullChecks": true, // 启用严格的 null 检查
        "noImplicitThis": true, // 当 this 表达式值为 any 类型的时候，生成一个错误
        "alwaysStrict": true, // 以严格模式检查每个模块，并在每个文件里加入 'use strict'

        /* 额外的检查 */
        "noUnusedLocals": true, // 有未使用的变量时，抛出错误
        "noUnusedParameters": true, // 有未使用的参数时，抛出错误
        "noImplicitReturns": true, // 并不是所有函数里的代码都有返回值时，抛出错误
        "noFallthroughCasesInSwitch": true, // 报告 switch 语句的 fallthrough 错误。（即，不允许 switch 的 case 语句贯穿）

        /* 模块解析选项 */
        "moduleResolution": "node", // 选择模块解析策略： 'node' (Node.js) or 'classic' (TypeScript pre-1.6)
        "baseUrl": "./", // 用于解析非相对模块名称的基目录
        "paths": {}, // 模块名到基于 baseUrl 的路径映射的列表
        "rootDirs": [], // 根文件夹列表，其组合内容表示项目运行时的结构内容
        "typeRoots": [], // 包含类型声明的文件列表
        "types": [], // 需要包含的类型声明文件名列表
        "allowSyntheticDefaultImports": true, // 允许从没有设置默认导出的模块中默认导入。

        /* Source Map Options */
        "sourceRoot": "./", // 指定调试器应该找到 TypeScript 文件而不是源文件的位置
        "mapRoot": "./", // 指定调试器应该找到映射文件而不是生成文件的位置
        "inlineSourceMap": true, // 生成单个 soucemaps 文件，而不是将 sourcemaps 生成不同的文件
        "inlineSources": true, // 将代码与 sourcemaps 生成到一个文件中，要求同时设置了 --inlineSourceMap 或 --sourceMap 属性

        /* 其他选项 */
        "experimentalDecorators": true, // 启用装饰器
        "emitDecoratorMetadata": true // 为装饰器提供元数据的支持
    }
}
```
