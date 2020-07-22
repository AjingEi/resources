## 一、执行上下文/作用域链/闭包/变量提升/this
### 执行上下文
**1.对执行上下文的理解**  

   执行上下文就是JavaScript 执行一段代码时的运行环境。

**2.对函数调用栈的理解**  

   用来管理函数调用关系的一种数据结构。  
   管理执行上下文的栈称为执行上下文栈，又称调用栈
### 作用域链
**3. 描述一下作用域链/谈谈你对作用域链的理解**

当查找变量的时候，会先从当前上下文的变量对象中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样由多个执行上下文的变量对象构成的链表就叫做作用域链。

**4. 怎么判断哪个是父级作用域**  

是根据词法作用域来判断的。词法作用域就是指作用域，是由代码中函数声明的位置来决定的，所以词法作用域是静态的作用域，通过它就能够预测代码在执行过程中如何查找标识符。

**5. 怎么理解作用域**   

作用域是指在程序中定义变量的区域，该位置决定了变量的生命周期。通俗地理解，作用域就是变量与函数的可访问范围，即作用域控制着变量和函数的可见性和生命周期。  

作用域主要分为两种：
- 全局作用域中的对象在代码中的任何地方都能访问，其生命周期伴随着页面的生命周期。
- 函数作用域就是在函数内部定义的变量或者函数，并且定义的变量或者函数只能在函数内部被访问。函数执行结束之后，函数内部定义的变量会被销毁。

ES6出现的：  
块级作用域就是使用一对大括号包裹的一段代码

### 闭包
**6. 闭包的使用场景**

除了 timer 定时器，事件处理，Ajax 请求等比较常见的异步任务，还有其他的一些异步 API 比如 HTML5 Geolocation，WebSockets , requestAnimationFrame()也将使用到闭包的这一特性。

需要存储一些私有变量的地方把


变量的生命周期取决于闭包的生命周期。被闭包引用的外部作用域中的变量将一直存活直到闭包函数被销毁。如果一个变量被多个闭包所引用，那么直到所有的闭包被垃圾回收后，该变量才会被销毁。

**7. 使用闭包需要注意什么**

如果引用闭包的函数是一个全局变量，那么闭包会一直存在直到页面关闭；但如果这个闭包以后不再使用的话，就会造成内存泄漏。

如果该闭包会一直使用，那么它可以作为全局变量而存在；但如果使用频率不高，而且占用内存又比较大的话，那就尽量让它成为一个局部变量。

**8. 闭包有什么作用**  

**9. 谈谈对闭包的理解**

在 JavaScript 中，根据词法作用域的规则，内部函数总是可以访问其外部函数中声明的变量，当通过调用一个外部函数返回一个内部函数后，即使该外部函数已经执行结束了，但是内部函数引用外部函数的变量依然保存在内存中，我们就把这些变量的集合称为闭包。比如外部函数是 foo，那么这些变量的集合就称为 foo 函数的闭包。



### 变量提升
 **10. 什么是变量提升**  

 所谓的变量提升，是指在 JavaScript 代码执行过程中，JavaScript 引擎把变量的声明部分和函数的声明部分提升到代码开头的“行为”。变量被提升后，会给变量设置默认值，这个默认值就是我们熟悉的 undefined。

 **11. 变量提升的实现、原因**  

 实际上变量和函数声明在代码里的位置是不会改变的，而且是在编译阶段被 JavaScript 引擎放入内存（上下文中的变量环境）中。（JS引擎执行有两个个阶段：编译和执行）

 **12. 什么是块级作用域**

块级作用域就是使用一对大括号包裹的一段代码

**13. var、let、const区别**  

使用 let 关键字声明的变量是可以被改变的，而使用 const 声明的变量其值是不可以被改变的  

let和const是块级作用域， 作用域块内声明的变量不影响块外面的变量。

作用域块中通过 let 声明的变量，会被存放在词法环境的一个单独的区域中，这个区域中的变量并不影响作用域块外面的变量

在词法环境内部，维护了一个小型栈结构，栈底是函数最外层的变量，进入一个作用域块后，就会把该作用域块内部的变量压到栈顶；当作用域执行完成之后，该作用域的信息就会从栈顶弹出，这就是词法环境的结构。

沿着词法环境的栈顶向下查询，如果在词法环境中的某个块中查找到了，就直接返回给 JavaScript 引擎，如果没有查找到，那么继续在变量环境中查找。

**14. es6了解不，说一下let、const的暂时性死区**

在块作用域内，let声明的变量被提升，但变量只是创建被提升，初始化并没有被提升，在初始化之前使用变量，就会形成一个暂时性死区。

var的创建和初始化被提升，赋值不会被提升。
let的创建被提升，初始化和赋值不会被提升。
function的创建、初始化和赋值均会被提升。

只不过通过let或者const声明的变量会在进入块级作用域的时被创建，但是在该变量没有赋值之前，引用该变量JavaScript引擎会抛出错误---这就是“暂时性死区”

 暂时性死去是语法规定的，也就是说虽然通过let声明的变量已经在词法环境中了，但是在没有赋值之前，访问该变量JavaScript引擎就会抛出一个错误。


参考文章：  
[[解惑文章:作用域和闭包](https://time.geekbang.org/column/article/127495)]

### this指向
**15. 一句话描述一下this**
this 就是一个指针，指向调用函数的对象

**16. 函数内的this是在什么时候确定的？**
引用的时候确定的
 
要判断this的话，主要根据调用函数的位置。  
主要分为四种：  
默认绑定：没有任何其他引用，直接关联window。  
隐式绑定：前面有对象引用，关联到对象。（但是隐式绑定很容易消失）  
显式绑定：call/apply/bind绑定  
new绑定：
箭头函数绑定this-----》下一个问题

**17. 使用箭头函数时需要注意什么**

- 箭头函数没有自己的this，它的this继承于外层代码库中的this    
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。   
- 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。  
- 不可以使用yield命令，因此箭头函数不能用作 Generator 函数。  
- 箭头函数没有自己的this，所以不能用call()、apply()、bind()这些方法去改变this的指向

**18. 箭头函数和普通函数的区别(同上)** 


## 一、原型/继承

主要使用到的函数
```
// 属性定义
Object.defineProperty(person, 'name', {
    configurable: false,
    value: 'jack'
})
Object.defineProperty(person, 'name', {
    set: function(){
        
    },
    get: function(){

    }
})
Object.definedProperties({

})
Object.getOwnPropertyDescriptor(person, 'name')

// 原型链
Person.prototype.isPrototypeOf(person1O)
Object.getPrototypeOf(person1) === Person.prototype // true
person1.hasOwnProperty('name')
person.__proto__ === Person.prototype
Person === Person.prototype.constructor
```

**19. 创建对象的方式**
- 工厂模式：
```
function CreatObject(){
    var o = new Object();
    o....
    return o
}
var person = CreatObject('')
```
- 构造函数模式：
```
function Person(name, age){
    this.name = name
    this.age = age
}
var person1 = new Person('jack', 11)
```
- 原型模式
```
function Person(){
}
Person.prototype.name = 'nico'
```
- 结合构造函数模式和原型模式:
     
构造函数用于定义实例属性，原型模式用于定义方法和共享的属性


**20. 谈谈你对JS 原型和原型链的理解？** 

JS 原型是指为其它对象提供共享属性访问的对象。在创建对象时，每个对象都包含一个隐式引用指向它的原型对象或者 null。

原型也是对象，因此它也有自己的原型。这样构成一个原型链。

**21. 原型链有什么作用？**

在访问一个对象的属性时，实际上是在查询原型链。这个对象是原型链的第一个元素，先检查它是否包含属性名，如果包含则返回属性值，否则检查原型链上的第二个元素，以此类推。

**22. 实现继承**
- 原型链继承：
```
function A(){
    this.name = 'jack'
}
A.prototype.getName = function (){
    console.log(this.name)
}
function B(){

}
B.prototype = new A;
B.Prototype.constructor = B

let b = new B
```
- 构造函数继承
```
function Parent(name) {
    this.name = [name]
}
Parent.prototype.getName = function() {
    return this.name
}
function Child() {
    Parent.call(this, 'zhangsan')   // 执行父类构造方法并绑定子类的this, 使得父类中的属性能够赋到子类的this上
}
```

- 寄生组合继承
```
function Parent(name) {
    this.name =name
}
Parent.prototype.getName = function() {
    return this.name
}
function Child() {
    // 构造函数继承
    Parent.call(this, 'zhangsan') 
}
//原型链继承
// Child.prototype = new Parent()
Child.prototype = Object.create(Parent.prototype)  //将`指向父类实例`改为`指向父类原型`
Child.prototype.constructor = Child
```

## 判断变量类型/变量相等

```
Object.prototype.toString.call({})       
```
[类型文章](https://juejin.im/post/5d030e03518825361817032f#heading-22)  
**23. 说一说javascript中有哪些数据类型?**

基本类型分为以下六种：
string（字符串）
boolean（布尔值）
number（数字）
symbol（符号）
null（空值）
undefined（未定义）

对象类型
对象类型也叫引用类型，array和function是对象的子类型。对象在逻辑上是属性的无序集合，是存放各种值的容器。对象值存储的是引用地址，所以和基本类型值不可变的特性不同，对象值是可变的。

**24. 说说你对javascript是弱类型语言的理解?**
JavaScript 是弱类型语言，而且JavaScript 声明变量的时候并没有预先确定的类型，变量的类型就是其值的类型，也就是说变量当前的类型由其值所决定,夸张点说上一秒种的String，下一秒可能就是个Number类型了，这个过程可能就进行了某些操作发生了强制类型转换。虽然弱类型的这种不需要预先确定类型的特性给我们带来了便利，同时也会给我们带来困扰，为了能充分利用该特性就必须掌握类型转换的原理。

**25. null和undefined的区别**  
null表示"没有对象"，即该处不应该有值。undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。

**26. typeof和instanceof的区别**

typeof表示是对某个变量类型的检测，基本数据类型除了null都能正常的显示为对应的类型，引用类型除了函数会显示为'function'，其它都显示为object。

而instanceof它主要是用于检测某个构造函数的原型对象在不在某个对象的原型链上。

**27. 详细说下instanceof**  

instanceof它主要是用于检测某个构造函数的原型对象在不在某个对象的原型链上。
```
friend instanceof Object
function myInstanceof (left, right) {
  let proto = Object.getPrototypeOf(left);
  while (true) {
    if (proto === null) return false;
    if (proto === right.prototype) return true;
    proto = Object.getPrototypeOf(proto)
  }
}
```
**28. typeof为什么对null错误的显示**  
这只是 JS 存在的一个悠久 Bug。在 JS 的最初版本中使用的是 32 位系统，为了性能考虑使用低位存储变量的类型信息，000 开头代表是对象然而 null 表示为全零，所以将它错误的判断为 object 。

**29. 说一下JS内置对象**


**30. 缩短白屏时长，可以有以下策略：**  
- 通过内联 JavaScript、内联 CSS 来移除这两种类型的文件下载，这样获取到 HTML 文件之后就可以直接开始渲染流程了。
- 但并不是所有的场合都适合内联，那么还可以尽量减少文件大小，比如通过 webpack 等工具移除一些不必要的注释，并压缩 JavaScript 文件。
- 还可以将一些不需要在解析 HTML 阶段使用的 JavaScript 标记上 sync 或者 defer。
- 对于大的 CSS 文件，可以通过媒体查询属性，将其拆分为多个不同用途的 CSS 文件，这样只有在特定的场景下才会加载特定的 CSS 文件。

## 异步

### promise

**微任务包括哪些，宏任务包括哪些**
微任务包括：MutationObserver、Promise.then()或catch()、Promise为基础开发的其它技术，比如fetch API、V8的垃圾回收过程
宏任务包括：script 、setTimeout、setInterval 、setImmediate 、I/O 、UI rendering。

**为什么会出现promise**

Promise 解决的是异步编码风格的问题/

**JS异步实现有哪些**


## 设计模式
**19. 说一下你知道的设计模式**  

工厂模式、观察者模式

**20. 具体说一下工厂模式**

工厂模式类似于现实生活中的工厂可以产生大量相似的商品，去做同样的事情，实现同样的效果;这时候需要使用工厂模式。

第一：弱化对象间的耦合，防止代码的重复。在一个方法中进行类的实例化，可以消除重复性的代码。第二：重复性的代码可以放在父类去编写，子类继承于父类的所有成员属性和方法，子类只专注于实现自己的业务逻辑。

**21. 观察者模式**  

它定义了对象间的一种一对多的关系，让多个观察者对象同时监听某一个主题对象，当一个对象发生改变时，所有依赖于它的对象都将得到通知。

# CSS
**盒模型**



## React 

**redux**  

应用中所有的 state 都以一个对象树的形式储存在一个单一的 store 中。 惟一改变 state 的办法是触发 action，一个描述发生什么的对象。 为了描述 action 如何改变 state 树，你需要编写 reducers。