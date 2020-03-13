---
layout: post
title: 手写call、apply、bind、深拷贝......
subtitle: '"Learning"'
date: 2020-03-03
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 2020
---

> “🙉🙉🙉 ”

## 正文

### call

自己实现 call 的话，我们要先搞清楚 call 实现了什么？

看一下示例代码：

```
let obj = {
    firstName: 'John',
    lastName: 'Doe'
}
let func = function(text) {
    console.log(text, this.firstName, this.lastName)
}
func('hello!')
// hello! undefined undefined
func.call(obj, 'hello?')
// hello? John Doe
```

显而易见，本来没有打 this.firstName 和 lastName 的函数，用 call 并传入有这两个属性的对象就成功打印出来了。所以 call 把函数中的 this 指向了传入的第一个参数，然后执行该函数。

我们要实现的话，要先了解一个知识点：如果一个函数作为一个对象的属性，那么通过对象的.运算符调用此函数，this 就是此对象。而在 js 里，函数就是一个对象，从 Function 对象继承而来的。那么结合上面两点，我们要实现 func.call(obj)的话，func 是对象，我们要调用这个 func 函数，并改变 this，那么我们只要在 obj 上新建一个函数，让这个函数等于 func 函数，然后再调用它不就行了？

```
Function.prototype.call2 = function(arg1){
    // 新建了函数，并等于我们要执行的那个函数，又因为是在arg1中执行的，所以this也就指向arg1，在这里也就是上文的obj
    arg1.newFunc = this;
    arg1.newFunc();
}
```

剩下就是一些小细节了，比如 call 如果传入的第一个参数为 null，那么 this 就会指向 window，那么我们只要在前面定义以下就可以了。

```
// 如果arg1为null 那么arg1为window
arg1 = arg1 || window
```

还有如果 func 的结果要 return 呢？那么我们就稍微改下

```
// arg1.newFunc();
return arg1.newFunc()
```

我们这边新建了一个函数，暂且称它为 newFunc，那么如果 obj 中这个函数已经存在了呢？我们不就覆盖了这个函数吗？

我找到了两种解决方法，1 是用 Math.random()随机生成一个 id，如果这个 id 已经存在于 person1 上，那么再生成一个 id，在最后删除它

代码：

```
var uniqueID = "00" + Math.random();
  while (context.hasOwnProperty(uniqueID)) {
    uniqueID = "00" + Math.random();
  }
arg1[uniqueID] = this;
......
delete context[uniqueID];
```

2 是用 不管之前存不存在，都新建一个对象，在其中保存下这个名字的函数，在最后再还原它

代码：

```
// 保存默认的newFunc
const { newFunc } = arg1;
......
// 恢复默认的fn
context.fn = fn;

```

然后我们要实现第二步：call 传入的第二个参数开始，均传入 newFunc 中。简单，只要知道函数有 arguments 这个属性就可以了，使用'[...arguments.slice(1)]'或者'Array.from(arguments).slice(1)'就可以了，如果不让使用 es6 特性，那么使用 eval，具体看下面代码：

```
var args = [];
for (var i = 1; i < arguments.length; i++) {
    args.push("arguments[" + i + "]");
}
var result = eval("context.fn(" + args + ")");
return result;
```

最后我们把所有代码组合起来：

```
Function.prototype.call2 = function(arg1) {
    if (typeof this !== "function") {
        throw new TypeError("Error");
    }

    // 默认上下文是window
    arg1 = arg1 || window;
    // 保存默认的fn
    const { newFunc } = arg1;

    // 前面讲的关键，将函数本身作为对象context的属性调用，自动绑定this
    arg1.newFunc = this;
    const args = [...arguments].slice(1);
    const result = arg1.newFunc(...args);

    // 恢复默认的fn
    arg1.newFunc = newFunc;
    return result;
};
```

### apply

apply 和 call 的唯一区别就是 apply 只能传入两个参数，第二个参数是一个列表，其中包含要传入执行的所有参数。那么我们上面使用 slice 截取参数都不用，因为一级参数个数已经确定，我们只要判断第二个参数是否存在并处理就可以了。

代码：

```
Function.prototype.myApply = function(arg1, arg2) {
  if(typeof this !== 'function') {
    throw new TypeError('Error')
  }

  arg1 = arg1 || window
  const {newFunc} = arg1

  arg1.newFunc = this
  let result
  if(Array.isArray(arguments[1])) {
    result = arg1.newFunc(...arguments[1])
  } else {
    result = arg1.newFunc()
  }

  arg1.newFunc = newFunc
  return result
}
```

### bind

bind 与前两者稍微有些不同，它结果是返回一个新的函数，其中的 this 已改变了指向。

### 深拷贝

我们都知道，实现一个对象的浅拷贝是很简单的有以下几种方法：

1. Object.assign(obj) ：实现一维数组的拷贝
2. JSON.parse(JSON.stringify(obj)) ：实现多维数组的拷贝，但是 undefined 和 symbol、函数在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 null（出现在数组中时）。

### 走台阶

---

## 后记

—— 24253 记于 2020-3-3
