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
- 