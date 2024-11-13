---
title: js面经
date: 2024-11-12 19:49:09
tags: 面经
---
# js面经

## this

在绝大多数情况下，函数的调用方式决定了this的值(运行时绑定).this{%label 不能在执行期间被赋值 red%}, 并且在每次函数被调用时this的值也可能会有不同。

### 如何确认this的值

在非严格模式下，总是指向一个对象，在严格模式下可以是任意值。

```js
// 为整个脚本开启严格模式
"use strict"

function func() {
    // 为函数开启严格模式
    "use strict"
}
```

1. 全局执行环境中,指向全局对象(非严格模式,严格模式)
2. 函数内部,取决于函数{%label 被调用 red%}的方式
   1. 直接调用的this的值:
      - 非严格模式: 全局对象
      - 严格模式: undefined
   2. 对象方法调用的this值
      - 调用者

### 如何指定this的值

1. 调用时制定

   1. call方法
   2. apply方法

   ```js
   func.call(thisArg,参数1,参数2...)
   func.apply(thisArg,[参数1,参数2...])
   ```

2. 创建时指定

   1. bind方法
   2. 箭头函数没有this,只能用上级作用域的this

   ```js
   const bindFunc = func.bind(thisArg,绑定参数1, 绑定参数2...)
   const itheima = {
       name: '波仔',
       eat() {
           setTimeout(()=>console.log(this));
       }
   }
   ```

### 手写call,apply,bind

