- 闭包
- 作用域
- 原型链
- 变量提升
- 函数参数值传递--- 浅拷贝
- this 指向问题--- 默认绑定/隐式绑定/硬绑定/new绑定
- 函数提升以及优先级问题  
  
由此可见函数提升要比变量提升的优先级要高一些，且不会被变量声明覆盖，但是会被变量赋值之后覆盖。
- new 操作符做了什么？
```
1. 创建一个空对象，构造函数中的this指向这个空对象
2. 这个新对象被执行 [[原型]] 连接
3. 执行构造函数方法，属性和方法被添加到this引用的对象中
4. 如果构造函数中没有返回其它对象，那么返回this，即创建的这个的新对象，否则，返回构造函数中返回的对象。

function new(){
    let target = {}
    let [construstors, ...args] = [...arguments]
    target.__proto__ = construstors.prototype
    let result = construstors.apply(target, ...args)
    if(result && (typeof result === 'object')){
        return result
    }
    return target
}
```
- 用 ES5 实现一个继承（有哪些方式）---寄生组合继承
- 0.2+0.1不等于0.3问题（浮点数精度）
```
function add(num1, num2) {
  const num1Digits = (num1.toString().split('.')[1] || '').length;
  const num2Digits = (num2.toString().split('.')[1] || '').length;
  const baseNum = Math.pow(10, Math.max(num1Digits, num2Digits));
  return (num1 * baseNum + num2 * baseNum) / baseNum;
}
```
- 堆、栈、队列是什么？都有什么区别？有什么应用？----算法复习
- 深拷贝、浅拷贝问题（immutable是怎么实现的？）
- typed array 问题
- es6 箭头函数问题
- let 会提升吗？声明、初始化、赋值等概念。什么是暂时性死区？
- 什么是 iterator？for of 用过吗？
- call、apply、bind 区别，bind 怎么实现的？
- caller、callee 了解吗？什么时候会用到？建议用吗？
- es6 其他特性用过吗？（Class、Map、Set、Decorator 等分别考察）
- promise 实现原理（怎么实现取消？怎么实现 promise all、race 等？）
- async await 知识点（await 的作用，async 返回的是什么）
- generator 又是什么？
- v8 线程模型、event loop（async、promise、nextTick、setTimeout、setImmediate 经典问题变着花样考）
- 进程和线程是什么？有什么区别？
- v8 垃圾回收机制
- 输入 URL，浏览器的执行过程又是怎么样的？（浏览器解析方式、顺序，async、defer等）
- 了解前端模块化吗？有几种规范？（commonjs 和 es module 都是怎么实现的？有啥区别？）



# css、html、dom、浏览器相关基础
- 盒模型
- 样式覆盖优先级问题  
浏览器缺省 < 外部样式表 < 内部样式表 < 内联样式   
类选择器 < 类派生选择器 < ID选择器 < ID派生选择器  

- 选择器相关问题
- 怎么解决边距重叠？（什么是 BFC？怎么创建 BFC？）
- flex 弹性布局了解吗？用过哪些？（问一些实际问题）
- 移动端的一些坑
- css modules 了解吗？
- sass、less 用过吗？用到了什么特性？实践情况
- 移动端用什么距离单位？（px、百分比、vw、vh、rem 等）
- 什么是逻辑像素，什么是物理像素，设备像素比又是什么？
- 事件捕获冒泡
- 哪些操作导致 reflow、repaint、composite
- 什么时候用 css 动画，什么时候用 transition？选择标准是什么？（如何知道动画执行结束了？）
- dom api 相关
- cookie、localStorage、sessionStorage 区别和使用场景
- 跨域相关问题，怎么解决？几种方式？
- 缓存相关（强缓存、协商缓存，由此引申 http 相关缓存知识）


# React
- React 事件机制
- 聊聊 React 的 diff
- React 优化
- 怎么理解闭包
- 节流怎么实现的

# 自己准备
- 手写call/apply/bind
```
Function.prototype.mycall = function (context) {
    context = context || window
    context.fn = this
    let argus = [...arguments].slice(1)
    let result = context.fn(...args)
    delete context.fn
    return result 
}
Function.prototype.myApply = function (context) {
    context = context || window
    context.fn = this
    let argus = [...arguments].slice(1)
    let result = context.fn(args)
    delete context.fn
    return result 
}
Function.prototype.mybind = function (context) {
  let self = this
  let args = [...arguments].slice(1)
  return function(){
      let newArg = [...arguments]
      return self.apply(context, args.concat(newArg))
  }
}

```
- 手写new

# 笔试准备
- 手写节流--(如果你持续触发事件，每隔一段时间，只执行一次事件。)如何对一个函数100ms内只执行一次
```
function throttle(fn, wait){
    let timeout;
    return function(){
        let context = this;
        let args = arguments
        if(!timeout){
            setTimeout(function(){
                timeout = null;
                fn.apply(context, args)
            }, wait)
        }
    }
}
```
- 手写防抖（当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，如果设定的时间到来之前，又一次触发了事件，就重新开始延时。）
```
function debounce(fn, wait) {
    let timeout;
    return function(){
        let context = this;
        let args = arguments;
        clearTimeout(timeout)
        setTimeout(function(){
            fn.apply(context, args)
        }, wait)
    }
}
```
- 继承/面向对象设计/ea6和es5的区别
```
function Person(name) {
    this.name = name;
}

Person.prototype =  {
    sayHello: function () {
        return 'hello, I am ' + this.name;
    },
    get name() {
        return 'kevin';
    },
    set name(newName) {
        console.log('new name 为：' + newName)
    }
}

Person.onlySayHello = function () {
    return 'hello'
};
```
- promise.all//链式调用
```
var p1 = Promise.resolve(1),
    p2 = Promise.resolve(2),
    p3 = Promise.resolve(3);
Promise.all([p1, p2, p3]).then(function (results) {
    console.log(results);  // [1, 2, 3]
});


function promiseAll(promises) {
  return new Promise(function(resolve, reject) {
    if (!isArray(promises)) {
      return reject(new TypeError('arguments must be an array'));
    }
    var resolvedCounter = 0;
    var promiseNum = promises.length;
    var resolvedValues = new Array(promiseNum);
    for (var i = 0; i < promiseNum; i++) {
      (function(i) {
        Promise.resolve(promises[i]).then(function(value) {
          resolvedCounter++
          resolvedValues[i] = value
          if (resolvedCounter == promiseNum) {
            return resolve(resolvedValues)
          }
        }, function(reason) {
          return reject(reason)
        })
      })(i)
    }
  })
}
```
- 手写并发
- 链表相关问题-相交
- 树/二叉树深度
- 栈-绝对路径的简化
- 斐波那契
- 排序和查找----二分查重
- 贪心---会议时间的重叠
- 最小崩溃版本-二分法
- 私有变量的实现
```
function myVal (val){
    return {
        set:function (newval) {
            val = newval
        },
        get:function (){
            return val
        }
    }
}

var obj = myval(1)

obj.set()
obj.get()
```
- fill函数，用递归的方式
```
function myfill(n, val){
    if(n===0) return []
    let arr = myfill(n-1, value)
    arr.push(val)
    return arr
}

function myfill(n, val, arr=[]){
    if(n==0)
      return arr
    return myfill(n-1, val, arr.concat(val));
}
```
- 谈实习经历(谈了很久这个，针对我实习开发过什么东西，从头到尾画图讲解，画数据结构画流程图，代码有什么可以优化的地方等等，那些培训伪造工作经历的可以歇菜了)

- redux
- react生命周期 -- -和vue的区别
- react性能优化
- react数据流
- react重新渲染
- racet的setstate
- react无状态组件
- 定时器
- 面向对象设计题/设计模块化系统
- 函数值传递
- 盒模型
- 私有变量
- react事件机制
- 设计模式-手写观察者模式
```
工厂模式
function creatObj(val){
    let obj = new Object();
    obj.val = val;
    return obj;
}
单例模式
function signle(fn){
    let result = null
    return function () {
        return  result || fn.apply(this, arguments)
    }
}
装饰模式
const xiaowang = people();
console.log(xiaowang.character);

function decorate(ctr) {
  ctr.height = 180;
  ctr.weight = 70;
  ctr.character = 'handsome';
  return ctr;
}
策略模式
const strategies = {
  S: function(salary) {
    return salary * 4;
  },
  A: function(salary) {
    return salary * 3;
  },
  B: function(salary) {
    return salary * 2
  }
}

const calculateBonus = function(level, salary) {
  return strategies[level](salary);
}

const staff1 = calculateBonus('S', 10000);
const staff2 = calculateBonus('A', 20000);

观察者模式
class Event {
  constructor() {
    this.events = [];
  }

  on(fn) {
    this.events.push(fn);
  }

  emit(data) {
    this.events.forEach(fn => {
      fn(data);
    })
  }

  // off方法我这里就不实现了，也比较简单
  off () {}
}

const event = new Event();
event.on(function(data) {
  console.log('我是第一个注册事件', data);
});
event.on(function(data) {
  console.log('我是第二个注册事件', data);
});
event.emit('已发送');
```
- 设计组件的方式
- 跨域--jsonp写法

- 模块系统
- 自己的项目-流程图
- MVVM

- css盒模型//设置背景颜色会是哪一部分
- flex
```
flow-grow: 0不方大/<1按比例/>1平分
flow-shrink: 0按比例缩小/0不缩小/
```
- BFC


```
white-space: nowrap; /* 1️⃣首先，强制文本不换行； */
  overflow: hidden; /* 2️⃣其次，隐藏溢出； */
  text-overflow: ellipsis; /* 
```

三篇手写题汇总:
[一](https://juejin.im/post/5d9eef20e51d45781332e961)
[二](https://juejin.im/post/5da09076f265da5bb065dec1)
[三](https://juejin.im/post/5dad327951882508652e525e#heading-7)