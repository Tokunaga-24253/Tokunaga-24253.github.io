---
layout: post
title: 前端面试常见问题自我梳理
subtitle: '"写下我的回答，以便翻阅"'
date: 2019-07-09
author: 24253
header-img: img/Work.jpg
catalog: true
tags:
  - 2019
  - 大学学习
---

> “🙉🙉🙉 ”

## 新：

根据[2020 秋招牛客网阿里前端面经](https://www.nowcoder.com/discuss/tag/134?order=3&type=2&expTag=3&query=)整理

## HTML：

#### 语义化（标签）

为了 html 代码有更好的可读性，可以做到从代码上来展示页面的结构。良好的语义化代码可以直接从代码上就能看出来那一块到底是要表达什么内容。
HTML5 新增的语义化标签：header、nav、footer、article、section、aside、main

##### HTML5 新标签

- header、nav、footer
- article、section、aside、main
- video、audio
- canvas、svg

#### 重绘重排的原理

- 重绘  
  由于节点的几何属性发生改变或者由于样式发生改变而不会影响布局的，称为重绘，例如 outline, visibility, color、background-color 等，重绘的代价是高昂的，因为浏览器必须验证 DOM 树上其他节点元素的可见性。
  /当 render tree 中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如 background-color。则就叫称为重绘。

- 回流  
  回流是布局或者几何属性需要改变就称为回流。回流是影响浏览器性能的关键因素，因为其变化涉及到部分页面（或是整个页面）的布局更新。一个元素的回流可能会导致了其所有子元素以及 DOM 中紧随其后的节点、祖先节点元素的随后的回流。
  /当渲染树的部分(或全部)因为元素的规模尺寸、布局，隐藏等改变而需要重新构建，这就称为回流(reflow)。在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。

- 回流必将引起重绘，而重绘不一定会引起回流。

#### 如果 DOM 下 100 个节点更新那会重排 100 次吗

不会回流一百次  
现代浏览器大多都是通过队列机制来批量更新布局，浏览器会把修改操作放在队列中，至少一个浏览器刷新（即 16.6ms）才会清空队列(队列化修改并批量执行来优化重排过程)，但是有些属性会强制浏览器进行回流操作，比如 offsetTop/Left/Width/Height、scrollTop/Left/Width/Height、clientTop/Left/Width/Height。

#### 浏览器渲染原理

1. 处理 HTML 标记并构建 DOM 树。
2. 处理 CSS 标记并构建 CSSOM 树。
3. 将 DOM 与 CSSOM 合并成一个渲染树。
4. 根据渲染树来布局，以计算每个节点的几何信息，将各个节点绘制到屏幕上。

---

##### 常见的浏览器-内核-引擎

- chrome - webkit / blink - v8
- firefox - gecko - spidermonkey
- safari - webkit - javascriptCore
- edge - edgeHTML - chakra
- ie - trident - chakra

#### 事件代理

为什么？  
因为给每个子元素添加一个事件，就会不断地与 dom 节点进行交互，访问 dom 次数越多，引起浏览器重绘与重排的次数也就越多，为了优化性能，运用事件代理的话，只要给父元素添加一次事件就可以了。  
原理:  
一些 dom 事件（比如 click，mousedown，mouseup，keydown，keyup，keypress。）具有冒泡属性：就是事件会一层层向上传播，那么有了这个机制，我们如果给外层的节点加 onclick 事件，如果内层的节点触发了这个事件，那么就会触发我们定义的事件。

#### 事件捕获和事件冒泡

捕获：以外部->里部的顺序执行事件

冒泡：以里部->外部的顺序执行事件

w3c 标准是事件触发后，会先从外部到内部进行一遍捕获过程，再从内部到外部进行一遍冒泡内容。

adEventListener()的第三个参数 true 为捕获阶段执行此事件，false 为冒泡阶段执行此事件。

##### 阻止冒泡

非 IE：window.event.cancelBubble = true;

IE: e.stopPropagation()

---

## CSS：

#### css 选择器/权重

#### 垂直水平居中：

1. margin 负值法(原始)  
   父盒子设置:position:relative/absolute  
   Div 设置: position:absolute; top: 50%;left: 50%; transform: translate(-50%，-50%);

2. 已知宽高 div 设置：position:absolute;top/left/bottom/right:0; margin: auto;

3. table-cell（待完善）  
   父盒子设置:display:table-cell; text-align:center;vertical-align:middle;  
   Div 设置: display:inline-block;vertical-align:middle;

4. 利用 flex/grid 布局
   将父元素设置为 display:flex/grid，并且设置 align-items:center;justify-content:center;

#### 怎么实现鼠标移动上去两秒后展开，移开两秒后慢慢回收的动画效果:

1. hover 和 animation delay？

2. onmouseover 和 onmouseout？

---

#### css3 的 position

有 relative、absolute、fixed、static(默认)、inherit、sticky(css3 新增)

---

#### css3 新增属性

- transition、animation、transform
- 选择器(:nth-child、:last-child 等)
- box-shadow
- border-image、border-radius
- background-size(指定图片大小 px/%/cover/contain)、background-clip(指定图片定位区域，但是是从起始点开始变化)、background-origin(规定图片定位区域,但是 content-box/padding-box/border-box)、background-repeat(重复 repeat/no-repeat/inherit))

---

#### BFC 是什么

BFC 意思是块级格式化上下文，是一个独立的渲染区域。
BFC 的特点有：

1. 内部盒元素按常规流排列；
2. 内部元素左边 margin 与容器左边 border 接触。
3. 容器里面的子元素不会影响到外面的元素。
4. 浮动元素不会和 BFC 叠加。
5. 计算高度时包含浮动元素的高度。

BFC 常用来消除与浮动元素的重叠、消除高度塌陷。

#### flex

```
display:flex;
flex-direction: row/column;
flex: 1;
flex-basis: 100px;  //就像width
flex-wrap: wrap/nowrap/wrapreverse;
flex-grow: 1;
flex-shrink: 1;
order: 1/2/3;
justify-content: flex-start/flex-end/center;
align-items: flex-start/flex-end/center;
align-content: flex-start/flex-end/center; (只对多行有效)
align-self: flex-start/flex-end/center;

```

---

####　清除浮动

1. overflow:hidden/auto;
2. 新建 div，clear：both
3. 父级定义 height
4. position：absolute
5. 父级定义:after{content:'';clear:both;display:block;}

---

#### 圣杯布局、双飞翼布局

答：两个都是实现一个三列布局，中间自适应，两边固定宽。  
中间部分 width：100% float：left
左/右部分 width：200px；float：left；margin-left/right：100%；（拉到上一行）

接下来圣杯布局用父元素 margin-left/right：200px；（或 padding）
左/右部分 position: relative;left/right: -200px;实现  
双飞翼用中间加 margin-left: 200px;margin-right: 300px;将 inner 挤到中间实现  
中间自适应，两边固定宽用 flex 和 grid 更容易实现。

---

#### 响应式（media）

写法:  
@media 设备类型 and （设备特征）{  
 div{width：200px；height：200px}  
}

```
@media screen and (max-width:720px) and (min-width:320px)
{ body{ background-color:red; } }
```

---

## JS：

#### JS 单线程

js 是单线程执行的，因为如果是多线程，操作 DOM 就会有错误。

#### EventLoop、宏队列、微队列

js 需要处理并发任务，所以需要事件循环。

- 浏览器事件环：
  所有的宏任务放在一个宏任务队列（即任务队列），**处理完一个**宏任务(从 sccript 开始)，将微任务队列（包含当时所有的微任务）压入任务队列（宏任务队列）并执行，之后再取下一个任务队列（宏任务）中的宏任务。

- node 事件环：

多一个 process.nextTick,是微任务，但是优先级比 promise 高。

详细看[这里](https://juejin.im/post/5c910c9f6fb9a070e25a5f56)

#### 基本数据类型

基本类型：Number/String/Boolean/Undefined/Null/Symbol(ES6)

引用类型：Object(Array/Date/RegExp)

---

#### 判断类型方法

typeof instanceof Object.prototype.toString

```
typeof(test)
```

```
test instanceof XXX
```

```
Object.prototype.toString.call(test)
```

---

#### typeof 和 instanceof

两者都是用来判断数据类型的。  
typeof 判断基础类型没问题，引用类型如 Array、Number、String 时会输出 object，无法准确判断。  
instanceof 可以成功判断出各种引用类型，但是无法判断基础类型，可以判断基础类型的引用对象。  
Object.prototype.toString.call()可以成功判断出基础类型和引用类型。

---

#### for in/of forEach

都是 for 循环的变种  
for in 和 for 循环一样是得到下标或者 key(可以作用于对象)  
for of 和 forEach 则是直接得到值(不能用于对象)  
for of 是 ES6 新出的。

```
const arrs = [1,2,3];
for (let i in arrs) {
  console.log(i,arrs[i]);
}
for (let i of arrs) {
  console.log(i);
}
arrs.forEach(i => console.log(i));
```

##### 有哪些遍历方法？

for forin forof forEach | some every Map

---

#### var、let、const 的区别

var 声明，其作用域是函数体的全部,会导致变量提升、重复声明等问题。  
let 和 const 声明的变量有作用域，存在暂时性死区。  
let 可以看成是 var 的更严格。  
const 声明的变量值不能改变，一般用来声明常量。
const 声明必须直接赋值。

编程中应该使用 const 来默认声明变量，只有碰到确定会更改值的话再用 let。

---

#### const 声明的对象的属性值可以修改吗？：

可以的，只要不更改对象的引用就行。

---

#### call/apply/bind:

##### js 的 bind、apply、call 有什么区别

通过 apply 和 call 改变函数的 this 指向，他们两个函数的第一个参数都是一样的表示要改变指向的那个对象，第二个参数，apply 是数组，而 call 则是 arg1,arg2...这种形式。  
通过 bind 改变 this 作用域会返回一个新的函数，这个函数里面有了绑定对象的属性。

apply:

```
applyTest = {
  num: 1
}
function test(a,b){
  console.log(this.name+a+b);
}
test.apply(applyTest,[1,2]);

```

call:

```
callTest = {
  num: 1
}
function test(a,b){
  console.log(this.name+a+b);
}
test.call(callTest,1,2);
```

bind:

```
bindTest = {
  num : 1
}
function test(a,b) {
  console.log(this.num+a+b)
}
var newBind = test.bind(bindTest);
newBind(1,2);

```

---

#### 介绍一下 typeof 和 instanceof

两者都是用来判断数据类型的。  
typeof 判断基础类型没问题，引用类型如 Array、Number、String 时会输出 object，无法准确判断。  
instanceof 可以成功判断出各种引用类型，但是无法判断基础类型，可以判断基础类型的引用对象。  
Object.prototype.toString.call()可以成功判断出基础类型和引用类型。（number 和 Number？）

---

### ES6

#### 对 es6 有什么了解？

ES6 是 ECMA 为 JavaScript 制定的第 6 个标准版本，也是目前最新的，包含了从 15 年提出的第一个版本到 19 年出的第五个版本。

---

#### 说说 ES6 的一些新特性

## 答: 箭头函数、const&let、symbol、块级作用域、promise、class、await&async、解构赋值、数组扩展(...)、模板字符串、Set、Map

#### symbol，怎么理解:

ES6 新出的基本数据类型 表示独一无二的值。  
一般用来作为唯一标识符，可以保证不会出现同名的属性
而且 Symbol 作为属性名，不会被常规方法遍历得到，即该属性不会出现在 for...in、for...of 循环中，也不会被 Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回，可以起到类似 Java 私有变量的作用，但是可以使用 Object.getOwnPropertySymbols 方法，可以获取指定对象的所有 Symbol 属性名。

---

#### 新数据结构 Set、Map

---

#### 数组方法 map、filter、reduce

- map：用来对数组中的每一个元素调用指定函数进行处理，返回一个新数组。
- filter：用来对数组进行过滤，过滤规则为制定函数，返回一个新数组，里面的元素均不满足过滤规则。
- reduce：用来对数组中的每个元素调用指定函数进行处理，返回最终的一个值，简单的实例就是累加。

---

#### 深/浅拷贝

浅拷贝：一般用 Object.assign(obj)  
深拷贝：  
基础：JSON.parse(JSON.stringify())  
进阶：function deepClone(target) {
if(typeof target === 'object') {
let newTarget = Array.isArray(target) ? [] : {};
for(const key in target) {
newTarget[key] = deepClone(target[key]);
}
} else {
return target;
}
}

---

#### 断点续传原理

---

#### 解构赋值

看[这里](https://segmentfault.com/a/1190000012469713)

---

#### new 操作符原理（手动实现 new 给出思路）

1. 创建一个空对象 obj，作为要返回的对象实例。
2. 然后把这个空对象的原型指向构造函数的 prototype 属性。
3. 把这个空对象赋值给构造函数内部的 this 关键词。
4. 一步步执行构造函数。

---

#### 箭头函数，箭头函数 this 问题，箭头函数是否可以被 new

箭头函数是 ES6 新出的一种函数形式。  
箭头函数中的 this 指向的是包裹箭头函数的环境的 this/指向定义时的环境，也就是说，在箭头函数中调用 this 时，仅仅是简单的沿着作用域链向上寻找，找到最近的一个 this 拿来使用。  
箭头函数不能被 new 来实例化。  
箭头函数的 this 不可变。  
箭头函数没有 arguments 对象。

---

#### ES6 数组新增方法

Array.map(根据 callback 函数，返回一个新数组)  
Array.filter(根据 callback，返回过滤后的数组)  
Array.from(将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历的对象（包括 ES6 新增的数据结构 Set 和 Map）)  
Array.of(用于将一组值，转换为数组，可用来新建数组)  
Array.every(判断数组中所有元素是否符合条件，返回 true/false)  
Array.some(判断数组中是否有元素符合条件，返回 true/false)  
Array.find/findIndex(返回数组中符合条件的第一个元素，否则就返回 undefined/这个方法是返回数组中符合条件的第一个元素的索引值，否则就返回-1)

---

#### ES6 箭头函数和普通函数区别：

箭头函数是 ES6 新出的一种函数形式。  
箭头函数中的 this 指向的是包裹箭头函数的环境的 this/指向定义时的环境，也就是说，在箭头函数中调用 this 时，仅仅是简单的沿着作用域链向上寻找，找到最近的一个 this 拿来使用。  
箭头函数不能被 new 来实例化，换句话说不能被作为构造函数。  
箭头函数的 this 不可变，不能用 call、bind、apply 来改变。  
箭头函数没有 arguments 对象，如果要用就用 rest 参数替代。

---

#### 对 promise 的理解，对 async 和 await 的理解：

promise 和 async/await 的区别看[这里](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/33)。

##### promise.all

可以加入多个 promise，等到所有 promise 都 resolve 才返回 resolve，或者其中一个 rejected 就返回 rejected

[实现](https://juejin.im/post/5c3d702ee51d4551b747f0ac)

##### aysnc、await 问怎么实现：

##### 问 generator 是啥···

##### es5 怎么搞 promise/手写一个 promise 怎么写：

#### 继承的几种方式:

父类：

```
function Father(name) {
  this.name = name || 'Father';
  this.walk = function(){
    console.log('walking!');
  }
}
```

- 原型继承

```
function Child() {
}
Child.prototype = new Father();
```

缺点：要想为子类新增属性和方法，要在继承语句之后执行，不能放到构造器中、无法实现多继承、创建实例时无法向父类构造函数传参。

- 构造函数继承

```
function Child() {
  Father.call(this);
}
```

缺点：只能继承父类构造函数中的属性和方法，不能继承父类原型中的属性和方法(原型链中无父类)、无法实现函数复用，每个子类都有父类实例函数的副本，影响性能。

- 组合继承

```
function Child() {
  Father.call(this);
}
Child.prototype = new Father();
```

缺点：解决了上两个的缺点，但是调用了两次父类构造函数，生成了两份实例，多消耗了一点内存

- 寄生组合继承

```
function Cat(name){
  Animal.call(this);
}
(function(){
  // 创建一个没有实例方法的类
  var Super = function(){};
  Super.prototype = Animal.prototype;
  //将实例作为子类的原型
  Cat.prototype = new Super();
})();
```

解决了组合继承的小缺点

---

#### 原型链的理解

当我们定义一个对象的时候，我们会发现这个对象可以使用很多我们没定义的方法。我们进一步查看这个对象会发现，其拥有一个**proto**属性，这个属性中有很多方法，比如 toString、hasOwnProperty 等。

对象通过这个属性指向这个对象的原型，这个原型有 constructor 属性，指向这个原型的构造函数，构造函数的 prototype 属性又指回这个原型，一个个对象通过他们的原型连接起来，就构成了原型链。

所有对象的顶层原型是 Object 对象，其原型是 null。所有函数的顶层原型是 Function 对象

---

#### 防抖和节流

答：防抖和节流是两种预防高频率触发事件（比如 scroll 和 resize）导致页面掉帧、影响用户体验的方法。  
防抖技术就是在一定时间内规定事件被触发的次数，用代码表示就是规定一个时间段，如果时间段内没有触发下一个 scroll 事件，那么才触发响应（callback）事件。  
节流是在防抖的基础上规定如果一个响应事件没有在一定时间段内触发过，那么就触发一次这个响应事件。
这样可以实现图片的懒加载等功能。

---

### 闭包:

#### JS 没有闭包的话会怎么样:

理论：

- 闭包用一句话来定义就是返回函数内部变量的函数。
- 具体讲就是 JS 中有函数作用域这个概念，函数作用域就是一个位于函数内部的私有域，函数可以访问外部环境的变量，但是外部环境无法访问函数内部定义的变量。
- JS 的内存回收机制使得如果函数内部没有闭包的话，函数在执行完后就在内存中被回收了，就再也无法访问其内部变量了。
- 闭包利用了作用域可以继承这个概念，使得闭包能够访问函数作用域，从而我们就能够通过闭包来访问函数作用域。

实践：
闭包随处可见，一个 Ajax 请求的成功回调，一个事件绑定的回调方法，一个 setTimeout 的延时回调，或者一个函数内部返回另一个匿名函数，这些都是闭包。简而言之，无论使用何种方式对函数类型的值进行传递，当函数在别处被调用时都有闭包的身影。

没有闭包的话

---

### JS 垃圾回收

答：JS 的垃圾回收机制的基本原理是：

> 找出那些不再继续使用的变量，然后释放其占用的内存，垃圾收集器会按照固定的时间间隔周期性的执行这一操作。
> 局部变量的生存周期是在函数声明和执行阶段，函数执行完毕后，局部变量就没有存在的必要了。全局变量会在浏览器关闭或进程关闭才能释放。  
> 但还有其他的较复杂场景(比如闭包、对象的相互引用)，垃圾回收器就没有那么容易的判断变量是否有用。  
> 目前在浏览器中有两种策略：

1. 标记清除：现代浏览器几乎都用这个垃圾回收算法。  
   当变量进入执行环境时，就标记这个变量为“进入环境”。当变量离开环境时，则将其标记为“离开环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到他们。  
   垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记。  
   然后，它会去掉环境中的变量以及被环境中的变量引用的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。  
   最后，垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间。  
   会出现内存碎片问题，可以优化为标记-整理。
2. 引用计数：不太使用。  
   此算法把“对象是否不再需要”简化定义为“对象有没有其他对象引用到它”。如果没有引用指向该对象（零引用），对象将被垃圾回收机制回收。  
   循环引用(互相引用)会引起内存泄漏问题。

## 详见：[这里](https://juejin.im/post/5c5ebc505188256219174f19)

---

#### 设计模式

看[这里](https://www.cnblogs.com/tugenhua0707/p/5198407.html)

---

## React/Vue：

#### react 的生命周期（React16）

每个组件都包含“生命周期方法”，你可以重写这些方法，以便于在运行过程中特定的阶段执行这些方法。你可以使用此生命周期图谱作为速查表。在下述列表中，常用的生命周期方法会被**加粗**。其余生命周期函数的使用则相对罕见。

挂载  
当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：  
**constructor()**  
static getDerivedStateFromProps()  
**render()**  
**componentDidMount()**

更新  
当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：  
static getDerivedStateFromProps()  
**shouldComponentUpdate()**  
**render()**  
getSnapshotBeforeUpdate()  
**componentDidUpdate()**

卸载  
当组件从 DOM 中移除时会调用如下方法：  
**componentWillUnmount()**

错误处理  
当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法：  
static getDerivedStateFromError()  
componentDidCatch()

PS: 函数组件严格来说没有生命周期函数，但社区有相关实现?

#### Vue 生命周期

- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destroyed

#### Vue 的双向绑定原理

通过发布者订阅者方式对数据进行劫持和监听，数据劫持的实现是使用 Object.defineProperty 方法，在方法里面定义 get 和 set 方法，set 方式是数据发生变化就会触发，所以我们通过在 set 方法里面进行对视图的更新就可以实现数据和识图的双向绑定了。

双向绑定主要分为两部分，数据劫持和发布者-订阅者。

- 数据劫持
  设置一个监听器 Observer 用来劫持并监听属性。
- 发布者-订阅者
  如果属性发生变化，Observer 就告诉订阅者 Watcher 看是否需要更新，因为有很多个订阅者，所以我们要一个消息订阅器 Dep 来专门收集这些订阅者并且在前两者之间进行统一管理。
  初始化时我们还需要一个 Compile 来扫描解析每个节点，来初始化模板数据和绑定节点相应的订阅器。

##### Vuex 数据更新流程

组件内通过 dispatch 来调用 actions，actions 中通过 commit 来触发 mutations，在 mutations 中使用逻辑来更改 state 中的数据，因为 vue 双向绑定的特效，state 中的数据变化了，相应视图也会更新。

#### jquery 与 vue/react 的区别：

jquery 是用来简化 dom 操作的库，vue/react 则是来构建整个网站应用的框架。

#### vue 和 react 的区别:

我有看过 vue 作者尤雨溪在知乎上对 vue 和 react 的优点分别是什么的回答，他在其中说 react 一开始的定位就是提出开发 ui 的新思路，他们抛弃了传统的 html/css/js 搭配，希望能够只用写 js 就能够开发 web 应用，希望开发者能够把精力放到应用逻辑上面去，而不是 dom 操作。可以说 react 改变了前端开发的惯用写法。

vue 一开始的定位则是降低前端开发的门槛，采用了传统的 html/css/js 三件套的写法。也同样具有很多 react 的精华之处比如虚拟 dom、不用操作 dom 等。

我个人觉得上手难度来说 vue 是比 react 容易的，vue 提供了更加简单好用的开发形式，而 react 的自由度更加的高，开发者能有更多的选择，但是也是一种烦恼，比如 css 的写法就有很多方式、组件本来标准是 class 现在可用 function 写法等。

如果让我选择，我会选择 vue，因为我觉得能写出简单易看懂的代码才是厉害的开发者。

#### router 的原理

SPA 应用最大的特点就是无刷新，页面交互是无刷新的，这是使用了 ajax 技术进行与异步请求。页面跳转也是不刷新的，这就用到了路由。路由的实现很简单，就是对 url 进行解析，发现变化后触发一个事件（这个事件在 html5 前是 hashchange 事件，但是 url 会出现一个#号，html5 提出了新的 api：pushState/replaceState/popState,），这个事件不会向服务器发送请求，从而也就不会使页面进行刷新，我们通过监听这个事件来实现页面的更新。

##### vuex 中数据变化发生的流程

vue 组件中触发 dispatch 方法，dispatch 触发相应的 action，action 触发相应的 mutation，然后 mutation 对 state 中的数据进行更新。

#### 虚拟 dom：

看[这里](https://www.cnblogs.com/ranyonsue/p/9831434.html)

---

#### diff 算法：

## 看[这里](https://www.cnblogs.com/ranyonsue/p/9831434.html)

#### vue/react 最近的新技术：

---

#### react 父子组件传参

答：[父子组件方法调用](https://juejin.im/post/59c150de51882529c44491e1)  
父组件向子组件传值：父组件把子组件处加上属性，属性值设置为要传递的值。  
子组件向父组件传值：先在父组件中写一个方法来接收子组件传过来的值，

#### PureComponent 知道吗

#### Redux 原理

---

## 前端工具：

#### babel 的编译原理，抽象语法树

#### 前端工程化:

#### MVVM 架构

是 model-view-viewmodel 的缩写。是一种设计思想，model 代表数据模型和业务逻辑；view 代表视图；viewmodel 是一个同步两者的中间人。

View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的， 因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反应到 View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

---

#### web worker：

---

## 网络：

#### 浏览器 DNS 查询

- 先查询本地 host 文件，看看有没有保存和请求的 URL 相对应的 ip 地址。
- 如果没有，向根 DNS 服务器进行询问，根 DNS 服务器根据 url 的顶级域名向对应的 DNS 服务器询问（比如顶级域名为 com，就向 comDNS 服务器询发送询问请求，响应的 DNS 服务器再向负责这个域名的 DNS 服务器询问，然后一路传输回正确的 IP 地址）

##### DNS 递归和迭代的区别呢？

### https 介绍一下

https 就是安全版本的 http，因为 http 传输是明文传输的，很容易使用一些工具就能截取下这些请求，并从中找到敏感信息。

简单来看，https 与 http 的区别就是： 在请求前，会建立 ssl 链接，确保接下来的通信都是加密的，无法被轻易截取分析

一般来说，如果要将网站升级成 https，需要后端支持（后端需要申请证书等），然后 https 的开销也比 http 要大（因为需要额外建立安全链接以及加密等），所以一般来说 http2.0 配合 https 的体验更佳（因为 http2.0 更快了）

具体加密过程:

1. 服务端和客户端协商产生一对公私钥，公钥无所谓，私钥只能由服务端知道。
2. 客户端向服务端发送信息时，使用服务端给他的公钥对信息进行加密，再发送给服务端。
3. 服务端接收到加密信息后，使用只有自己知道的密钥对密文进行解密，得到明文。
4. 有时候为了防止受到中间人攻击，发送信公钥的的一方会产生一个数字签名，和公钥一起发送给对方，对方对数字签名进行验证，确定信息（公钥）来源的有效性。

---

---

#### http0.9/1.0/1.1/2.0

- http0.9:
  提供超文本传输功能、没有请求头、只支持 GET 请求

- http1.0:
  在 0.9 基础上增加了 header（状态码、content-type）、不再只能传输超文本文件了（脚本、样式、媒体文件）、支持 GET/HEAD/POST

* htpp1.1:
  在 1.0 基础上使能复用同一个 TCP 连接来完成多次请求/响应（在 HTTP 0.9 和 1.0 中，TCP 连线在每一次请求/回应对之后关闭。在 HTTP 1.1 中，引入了保持连线的机制，一个连接可以重复在多个请求/回应使用。持续连线的方式可以大大减少等待时间，因为在发出第一个请求后，双方不需要重新运行 TCP 握手程序。）、支持 GET/HEAD/POST/PUT/DELETE/TRACE/OPTIONS、重大的性能优化（分块传输、更好的缓存机制）、能够使不同域名配置在同一个 IP 地址的服务器上
  是**目前主流方法**

* http2.0:
  - 二进制分帧（在应用层(HTTP)和传输层(TCP)之间加了一个二进制分帧层，将所有传输内容分割为消息和帧，以消息的形式发送，消息由多个帧组成）
  - 首部压缩（要求字段转换为键值对的形式，用表来存储这些键值对，对于相同的数据，不再重复请求响应发送，请求响应的内容要不是新的键值对，要不是替换之前的键值对）
  - 多路复用（基于二进制分帧层，并行交错地发送多个响应/请求，使多个请求/响应互不影响干扰。所有通信都在一个 TCP 连接上完成，此连接可以承载任意数量的双向数据流。所以，如果 http2.0 全面应用，很多 http1.1 中的优化方案就无需用到了（譬如打包成精灵图，静态资源多域名拆分等））
  - 请求优先级（如果流被赋予了优先级，它就会基于这个优先级来处理，比如客户端设置 css>js>jpg，那么服务端按此顺序返回资源）
  - 服务器推送（服务器可以对一个客户端的请求发送多个响应，不用客户端明确进行请求，比如请求 html 资源，服务端返回 html 资源的同时返回 js 和 css 资源）
  - 流量控制（）

---

#### TCP 三次握手，四次挥手？

答：C 发起请求连接 S 确认，也发起连接 C 确认我们再看看每次握手的作用：第一次握手：S 只可以确认 自己可以接受 C 发送的报文段第二次握手：C 可以确认 S 收到了自己发送的报文段，并且可以确认 自己可以接受 S 发送的报文段第三次握手：S 可以确认 C 收到了自己发送的报文段

---

#### tcp 和 udp 区别，udp 使用场景

（1）TCP 是面向连接的可靠性传输，UDP 则是无连接、不保证可靠交付。  
（2）TCP 是面向字节流，UDP 面向报文。  
（3）TCP 只能是 1 对 1 的，UDP 支持 1 对 1,1 对多。  
（4）TCP 的首部较大为 20 字节，而 UDP 只有 8 字节。

udp 一般用于即时通信（对速度要求高与数据准确性和丢包要求）、在线视频、网络电话。

##### TCP 头部具体有哪些报文信息

---

#### http 报文的格式:

报文一般包括了：通用头部，请求/响应头部，请求/响应实体

- 通用头部  
  这也是开发人员见过的最多的信息，包括如下：  
  Request Url: 请求的 web 服务器地址  
  Request Method: 请求方式  
  （Get、POST、OPTIONS、PUT、HEAD、DELETE、CONNECT、TRACE）  
  Status Code: 请求的返回状态码，如 200 代表成功  
  Remote Address: 请求的远程服务器地址（会转为 IP）

- 请求/响应头部  
  常用的请求头部（https://dailc.github.io/2018/03/12/whenyouenteraurl.html）：  
  Content-Type：客户端发送出去实体内容的类型  
  常用的响应头部（https://dailc.github.io/2018/03/12/whenyouenteraurl.html）：  
  Access-Control-Allow-Headers: 服务器端允许的请求 Headers  
  Access-Control-Allow-Methods: 服务器端允许的请求方法  
  Access-Control-Allow-Origin: 服务器端允许的请求 Origin 头部（譬如为\*）  
  Content-Type：服务端返回的实体内容的类型

- 请求/响应实体  
  http 请求时，除了头部，还有消息实体，一般来说  
  请求实体中会将一些需要的参数都放入进入（用于 post 请求）。  
  譬如实体中可以放参数的序列化形式（a=1&b=2 这种），或者直接放表单对象（Form Data 对象，上传时可以夹杂参数以及文件），等等  
  而一般响应实体中，就是放服务端需要传给客户端的内容  
  一般现在的接口请求时，实体中就是对于的信息的 json 格式，而像页面请求这种，里面就是直接放了一个 html 字符串，然后浏览器自己解析并渲染。

---

##### 请求方式的具体作用

- GET GET 请求会**请求指定的资源**。
- HEAD HEAD 方法与 GET 方法一样，都是向服务器发出指定资源的请求。但是，服务器在响应 HEAD 请求时不会回传资源的内容部分(即响应主体)。这样我们可以获取服务器的响应头信息。HEAD 方法常被**用于客户端查看服务器的性能**。
- POST POST 请求会向指定资源提交数据，请求服务器进行处理，如：表单数据提交、文件上传等，请求数据会被包含在请求体中。POST 方法是非幂等的方法，因为这个请求可能会**创建新的资源或/和修改现有资源**。
- PUT PUT 请求会身向指定资源位置上传其最新内容，PUT 方法是幂等的方法。通过该方法客户端可以**将指定资源的最新数据传送给服务器取代指定的资源的内容**。
- DELETE DELETE 请求用于请求服务器删除所请求 URI（统一资源标识符，Uniform Resource Identifier）所标识的资源。DELETE 请求后**指定资源会被删除**，DELETE 方法也是幂等的。
- CONNECT CONNECT 方法是 HTTP/1.1 协议预留的，能够**将连接改为管道方式的代理服务器**。通常用于 SSL 加密服务器的链接与非加密的 HTTP 代理服务器的通信。
- OPTIONS OPTIONS 请求与 HEAD 类似，一般也是用于**客户端查看服务器的性能**。 这个方法会请求服务器返回该资源所支持的所有 HTTP 请求方法，该方法会用'\*'来代替资源名称，向服务器发送 OPTIONS 请求，可以测试服务器功能是否正常。XMLHttpRequest 对象进行 CORS 跨域资源共享时，就是使用 OPTIONS 方法发送嗅探请求，以判断是否有对指定资源的访问权限。
- TRACE TRACE 请求**服务器回显其收到的请求信息**，该方法主要用于 HTTP 请求的测试或诊断。
- PATCH 请求与 PUT 请求类似，二者有以下两点不同：1.PATCH 一般**用于资源的部分更新**，而 PUT 一般用于资源的整体更新。2.当资源不存在时，PATCH 会创建一个新的资源，而 PUT 只会对已在资源进行更新。

---

#### 手写原生 ajax

```
// creat
var xhr = new XMLHttpRequest();

// request callback
xhr.onReadyStateChange = function() {
  if( xhr.readyState == 4 ) {
    // check status code
    if( xhr.status >= 200 && xhr.status<300 || xhr.status == 304 ) {
        console.log(xhr.responseText);
    } else {
      // error
      ......
    }
  }
}

// GET
xhr.open('GET',url);
xhr.send();

// POST
xhr.open('POST',url);
xhr.send(data);

```

---

#### 状态码

答：

- 1xx：信息，请求收到，继续处理
- 2xx：成功，行为被成功地接受、理解和采纳
- 3xx：重定向，为了完成请求，必须进一步执行的动作  
  301；永久重定向
  302：临时重定向
- 4xx：客户端错误，请求包含语法错误或者请求无法实现
  400：请求存在语法错误
  401：请求未认证
  403：缓存可用
- 5xx：服务器错误，服务器不能实现一种明显无效的请求  
  500：服务器发生错误
  502：网关发生错误

##### 状态码 304（强缓存和协商缓存）

是状态码的一种，代表了客户端的缓存资源有效，不需要再次请求。

#### 强缓存和协商缓存

强缓存和协商缓存我理解都是浏览器缓存的一种策略。
当浏览器第一次访问一个页面的时候，因为是第一次，所以没有缓存过这个页面，于是浏览器向服务器发送请求，服务器响应这个请求，在响应的同时对于缓存的细节进行协商(是否要启用 Expires 或 Cache-Control(还是同时启用)，服务端发送 Etag、Last-Modified)，浏览器最后成功呈现页面。  
当浏览器再一次访问这个页面时，会先检查保存的缓存的 header 信息，然后根据 header 中的 Expires 和 Catch-Control 来判断此缓存是否过期。（Expires 是保存一个代表资源失效的绝对时间，如果双方时间不一致会导致混乱，Catch-Control 中的 max-age 值保存一个相对时间，可以有效的标志资源是否过期，catch-control 还有其他值能设置，比如设置不使用强缓存、禁止所有缓存、设置缓存权限等）
没过期的话会直接从缓存中获取页面并呈现。
过期的话，会向服务器发送请求，请求中包括上一次服务器端发送过来的 ETag 和 Last-Modify 所生成的 If-None-Match 和 If-Modify-Since，服务器根据这两个值判断缓存是否有效。（先对比 ETag，ETag 没问题，就继续对比 Last-Modify）
如果有效，返回 304，会返回新的 ETag，但是不会返回 Last-Modify。
过期则返回新的资源。
ETag 的作用是解决 Last-modify 无法解决的几个问题:

1. 文件周期性更改，导致内容不改变（仅仅修改时间改变了）
2. 文件在 1 秒内修改多次，而 Last-Modify 无法判断秒以下的精度。
3. 某些服务器无法精确的到修改时间。

具体看[这个](https://segmentfault.com/a/1190000008956069)

---

#### 跨域的理解：

跨域是一种浏览器出于安全方面考虑而作出的限制。如果在不符合同源策略的条件下进行请求，就会产生跨域问题。

看[这里](https://segmentfault.com/a/1190000012469713)

#### 实现跨域的方法

- 最经典的 JSONP
  利用 script 标签不受同源策略限制的特点来实现跨域，优点：实现简单、兼容性好。缺点：只支持 GET 请求、有安全性问题、需要服务端进行配合改造。

- 最流行的方法 CORS
  是目前主流的跨域解决方案。在后端设置 Access-Control-Allow-Origin 等字段来允许字段中的域名进行跨域请求，如果字段设置为\*，那么所有的跨域请求都可以进行。

- 其他
  - Nginx 反向代理（请求发给 nginx，nginx 作为代理服务器转发请求给服务器，这样就规避了同源策略）
  - window.name
  - document.domain(只能用于二级域名相同的情况下，比如 a.test.com 和 b.test.com)
  - location.hash
  - Websocket

##### JSONP 实现

---

#### 输入 url 到显示出来的过程：

1. 用户输入 URL，
2. 浏览器开始对 URL 进行解析（URL 分成协议+域名+，比如*https://www.baidu.com*）
3. 对把 URL 解析完毕后，得到了 DNS 地址，然后进行 DNS 查询。（查询有规则,下面有）
4. DNS 查询完毕，得到了此域名所对应的 IP 地址。然后对此 IP 地址进行 TCP 请求，进行 TCP 三次握手，建立连接。（三次握手具体：① 客户端向服务器发出请求。② 服务端接收到请求，并向客户端回复请求。③ 客户端收到服务端的回复，再次回复服务端。经过三次握手，客户端和服务端都确认了自己和对方的收发请求能力，这也是三次握手的作用，确认无误后就能开启 http 交互了）
5. 三次握手成功后，客户端查询本地缓存，如未发现过期，就使用本地缓存的页面进行渲染。如果发现缓存的资源过期或者未查询到缓存（可能是第一次访问），就向服务端发送 http 请求，请求头中附带 etag 和 if-modified（？），服务端收到请求，查看请求头中的信息，如果有的话对 etag 和 if-modified 进行比对，如果发现过期或者是第一次访问，就进行回复，状态号 200，请求主体是资源。如果发现未过期，就回复 304，说明资源未过期，请求头带新的 etag 和 if-modified，请求主体不带资源。
6. 客户端收到回复，如果 304 的话就更新 etag 和 if-modified。不然就根据返回主体中的资源渲染页面。（渲染页面先根据 html 文件渲染 dom 树，遇到 css、js 和其他资源都会向服务端进行请求，然后分别构建 dom 树和 css 树，再把两个树进行合并生成 render 树，根据 render 树对页面进行渲染）
7. 渲染完毕后（？），与服务器进行 4 次挥手，断开连接（4 次挥手具体：）。

看[这里](https://dailc.github.io/2018/03/12/whenyouenteraurl.html)

---

#### dns 解析过程：

DNS 的工作原理及过程分下面几个步骤：

1. 客户机提出域名解析请求，并将该请求发送给本地的域名服务器。
2. 当本地的域名服务器收到请求后，就先查询本地的缓存，如果有该纪录项，则本地的域名服务器就直接把查询的结果返回。
3. 如果本地的缓存中没有该纪录，则本地域名服务器就直接把请求发给根域名服务器，然后根域名服务器再返回给本地域名服务器一个所查询域(根的子域) 的主域名服务器的地址。
4. 本地服务器再向上一步返回的域名服务器发送请求，然后接受请求的服务器查询自己的缓存，如果没有该纪录，则返回相关的下级的域名服务器的地址。
5. 重复第四步，直到找到正确的纪录。
6. 本地域名服务器把返回的结果保存到缓存，以备下一次使用，同时还将结果返回给客户机。

---

#### session 和 cookie

cookie 是服务器发送到浏览器并保存的一块数据，下次浏览器向服务器发出请求时会被携带。用于保持用户的登录状态。cookie 的出现使无状态的 http 协议可以记录状态信息，大小不能超过 4K。

主要存储:

- 会话状态（登陆状态、购物车信息、游戏分数等）。
- 个性化设置。
- 行为跟踪。

session 是保存在服务端的。客户端请求创建一个 session 的时候，服务器检查请求中是否包含 sessionId，是的话就在本地检索并拿出来使用，无的话就创建一个 cookie 并生成一个相关联的 sessionId，并返回一个包含这个 sessionId 的 cookie 给客户端保存，客户端下次请求带上这个 sessionId 就行。

主要存储：

- 网上商城的购物车;
- 保存用户登录信息，防止用户非法登录;
- 将某些数据放入 session 中,供同一用户的不同页面使用;

##### sessionStorage 和 localStorage

两者都是 HTML5 新增的两个特效，主要是用来作为会话存储以及本地存储来使用的，解决了以往的 cookie 存储空间不足的问题，两者大小可以达到 5M。

sessionStorage 用于存储当前会话的数据，会话结束时会被清除。

localStorage 用于存储当前站点的数据，除非用户调用 api 清除或清除浏览器缓存，否则会被长期保存。

api：

- setItem(xx,xx);
- getItem(xx,xx);

##### 怎么设置 cookie 过期时间

---

## 安全：

#### csrf、xss，如何预防

答：  
xss(cross site script)也叫跨站脚本攻击，是通过漏洞往网站写入脚本来实现攻击。攻击方式有反射型(url 或其他输入点注入)和存储型(存储到数据库后读取时注入)。理论上所有用户输入点都有可能存在 xss 漏洞。  
防御：

- 过滤用户输入
- 对 cookie 进行安全操作(设置成 httponly，这样 js 就不能获取到该网站的 cookie 了)

csrf(cross site request forgery)也叫跨站请求伪造，就是让用户在不知情的情况，冒用其身份发起了一个请求。比如诱导用户点击一个攻击网址，攻击网址向被攻击网址发送请求，如果浏览器中存在此网站 cookie，那么被攻击网址就会识别是用户操作，从而被攻击。  
防御：

- 验证 HTTP Referer 字段(它记录了该 HTTP 请求的来源地址)
- 设置验证码
- 在 http 头中添加 token
- 对 cookie 进行安全操作(设置成 httponly，这样 js 就不能获取到该网站的 cookie 了)

---

## 性能优化：

#### 重绘与回流优化：

**CSS：**

1. 使用 transform 替代 top

2. 使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局

3. 避免使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局。

4. 尽可能在 DOM 树的最末端改变 class，回流是不可避免的，但可以减少其影响。尽可能在 DOM 树的最末端改变 class，可以限制了回流的范围，使其影响尽可能少的节点。

5. 避免设置多层内联样式，CSS 选择符从右往左匹配查找，避免节点层级过多。

```
<div>
  <a> <span></span> </a>
</div>
<style>
  span {
    color: red;
  }
  div > a > span {
    color: red;
  }
</style>
```

对于第一种设置样式的方式来说，浏览器只需要找到页面中所有的 span 标签然后设置颜色，但是对于第二种设置样式的方式来说，浏览器首先需要找到所有的 span 标签，然后找到 span 标签上的 a 标签，最后再去找到 div 标签，然后给符合这种条件的 span 标签设置颜色，这样的递归过程就很复杂。所以我们应该尽可能的避免写过于具体的 CSS 选择器，然后对于 HTML 来说也尽量少的添加无意义标签，保证层级扁平。

5. 将动画效果应用到 position 属性为 absolute 或 fixed 的元素上，避免影响其他元素的布局，这样只是一个重绘，而不是回流，同时，控制动画速度可以选择 requestAnimationFrame，详见探讨 requestAnimationFrame。

6. 避免使用 CSS 表达式，可能会引发回流。

7. 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点，例如 will-change、video、iframe 等标签，浏览器会自动将该节点变为图层。

**JavaScript:**

1. 避免频繁操作样式，最好一次性重写 style 属性，或者将样式列表定义为 class 并一次性更改 class 属性。
2. 避免频繁操作 DOM，创建一个 documentFragment，在它上面应用所有 DOM 操作，最后再把它添加到文档中。
3. 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
   对具有复杂动画的元素使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁回流。

---

#### CSS 对网页性能优化

- 将 CSS 代码放在 HTML 页面的顶部
- 避免使用 CSS 表达式
- 使用 < link> 来代替 @import
- 避免使用 Filters

---

#### 有没有考虑对图片处理的优化手段，说说常用的

- 优化图片大小，对图片进行压缩。
- 通过 CSS Sprites 优化图片
- 不要在 HTML 中使用缩放图片
- favicon.ico 要小而且可缓存
- 懒加载和预加载

#### 图片懒加载怎么做

1.  img 不设置 src 属性，先设置 data-src

2.  1.  通过 document.documentElement.clientHeight 获取屏幕可视窗口高度
        通过 element.offsetTop 获取元素相对于文档顶部的距离
        通过 document.documentElement.scrollTop 获取浏览器窗口顶部与文档顶部之间的距离，也就是滚动条滚动的距离
        然后判断 ②-③<① 是否成立，如果成立，元素就在可视区域内。
    2.  function isInSight(el) {
        const bound = el.getBoundingClientRect(); 图片到可视区域顶部距离
        const clientHeight = window.innerHeight; 可视区域的高度
        //如果只考虑向下滚动加载
        //const clientWidth = window.innerWeight;
        return bound.top <= clientHeight + 100;
        }
    3.  用到 intersectionRatio 来判断是否在可视区域内，当 intersectionRatio > 0 && intersectionRatio <= 1 即在可视区域内。

3.  绑定 scroll 事件，触发时对图片进行检查，是否在可视区域内。

---

#### 考虑过缓存方面的优化吗，强缓存和协商缓存区别

- 使用 Ajax 缓存
- 设置 ETag：ETags（Entity tags，实体标签）是 web 服务器和浏览器用于判断浏览器缓存中的内容和服务器中的原始内容是否匹配的一种机制。
-

---

#### React 性能优化

答：[这里](https://juejin.im/post/5d045350f265da1b695d5bf2)

---

#### 内容优化

- 减少 HTTP 请求数。这条策略是最重要最有效的，因为一个完整的请求要经过 DNS 寻址，与服务器建立连接，发送数据，等待服务器响应，接收数据这样一个消耗时间成本和资源成本的复杂的过程。
  常见方法：合并多个 CSS 文件和 js 文件，利用 CSS Sprites 整合图像，Inline Images (使用 data：URL scheme 在实际的页面嵌入图像数据 )，合理设置 HTTP 缓存等。
- 减少 DNS 查找
- 避免重定向
- 懒加载组件，预加载组件
- 减少 DOM 元素数量。页面中存在大量 DOM 元素，会导致 javascript 遍历 DOM 的效率变慢。
- 最小化 iframe 的数量。iframes 提供了一个简单的方式把一个网站的内容嵌入到另一个网站中。但其创建速度比其他包括 JavaScript 和 CSS 的 DOM 元素的创建慢了 1-2 个数量级。
- 减小 Cookie 大小

- 使用内容分发网络（CDN）。把网站内容分散到多个、处于不同地域位置的服务器上可以加快下载速度。
- GZIP 压缩
- 提前刷新缓冲区
- 对 Ajax 请求使用 GET 方法

- 将 JavaScript 脚本放在页面的底部。
- 将 JavaScript 和 CSS 作为外部文件来引用。在实际应用中使用外部文件可以提高页面速度，因为 JavaScript 和 CSS 文件都能在浏览器中产生缓存。
- 最小化 JavaScript 和 CSS 文件（webpack 等工具），优质的编码方式（比如使用事件监听）
- 尽量减少 DOM 的访问。访问 DOM 元素比较慢。
- javascript 代码注意：谨慎使用 with，避免使用 eval Function 函数，减少作用域链查找。

---

## 移动端：

---

## 可视化

## Node/后端：

#### 介绍一下 express：

---

## 算法

#### 有哪些排序方法:

冒泡排序、归并排序、插入排序、快速排序、堆排序

##### 快速排序原理

```

```

---

#### 查找算法

##### 一亿个订单找出金额最大的一万个数用什么方法时间复杂度和空间复杂度最低：

排序？考察查找算法

---

#### 链表

##### 判断链表是否有环

使用双指针，一个一次走一格，另一个走两格，如果有环，经过 n(环长度)次后，双指针会指向同一节点。

---

## 项目：

#### 说说项目中遇到的最大的困难

#### 项目中有考虑到哪些优化的地方？

---

## 其他问题：

#### 前端新技术

**WebAssembly**

#### 自我介绍：

大三上选择了前端作为我的职业方向，主要通过自学来学习前端，学习了大半年，自认为在 web 前端方向有了一定的知识基础和能力。现在希望在秋招能找到一份心仪的工作，同时也能同时也检验一下我的知识水平和学习成果，这次面试能过最好，不过的话也希望能暴露出自身的一些缺陷并改进。

1. 个人介绍（基本情况） 你好，我叫徐宇超，现在在浙江工商大学读大四，在校专业是信息安全。
2. 擅长什么，包括技术和非技术上的。技术上可以了解的你的专长，非技术上可以了解到你这个人；
3. 做过什么事。捡最主要的说，别把所有的项目都背书似的介绍一个遍；
4. 自己的一些想法、兴趣或者是观点，甚至包括自己的职业规划。这里主要是给面试官一个感觉就是你的确是热衷于“折腾”或者“思考”。就是这样，谢谢。

---

#### 为什么学前端？

因为前端比安全、后端更有趣，做的大部分都是看得见摸得着的东西因此正反馈更快(多)，更贴近用户，更看好其前景。

---

#### 怎么学前端的/说说你学前端的历程吧

刚开始是在 w3school 这个网站上学 html、css 和 js 的基础知识。  
后来做了几个很小的网站，有点急，想提前进入框架学习，看了一遍 vue 官网的文档，发现大部分东西都看不懂。于是回去重学基础，找到《js 高级程序设计》这本书囫囵吞枣地看了一遍。  
再后来发现视频学习比较有趣，去 Youtube 上看了很多教学视频，看他们如何从零开始建立一个网站，学到了很多新东西比如 sass、响应式设计等。  
现在也有学习去看官方的文档来学习一个东西。

#### 有什么要问的：

- 如果入职的话，需要我去学习什么

---

## 旧：

()怎么理解前后端分离思想

()怎么同时让多个异步请求并行？

树的深度优先遍历、广度优先遍历实现和区别

一棵二叉树要用数组存储，这棵树要具备哪种条件？ （完全二叉树）

实现括号匹配用数据结构怎么做？说说思路 （栈）

react hooks

Vue MVVM 原理

服务端渲染原理

在做项目时，有没有从架构层面考虑过？

我现在有个需求，需要实现一个 web 端的微信，你想想该怎么实现

怎么看待前后端分离思想，以及服务端渲染技术

你有什么想问的吗？

---

## 后记

—— 24253 记于 2019-7-9
