三篇手写题汇总:
[一](https://juejin.im/post/5d9eef20e51d45781332e961)
[二](https://juejin.im/post/5da09076f265da5bb065dec1)
[三](https://juejin.im/post/5dad327951882508652e525e#heading-7)


防抖和节流
```
function debounce(fn, wait){
    let timout = null;
    return function (){
        let context = this
        let args = [...arguments]
        clearTimeOut(timout)
        setTimeOut(function(){
            fn.apply(this, args)
        }, wait)
    }
}

function throttle(fn, wait){
    let timeout = null;
     return function (){
        let context = this
        let args = [...arguments]
        if(!timeout){
            setTimeOut(function(){
                timeout = null
                fn.apply(this, args)
        }, wait)
        }
    }
}
```
深拷贝
```
function deepClone (obj){
    var result = Array.isArray(obj) ? [] : {};
    for(let key in obj ){
        if(obj.hasOwnPropotype(key)){
            if(typeof key === 'object' && obj[key] !== null ){
               result[key] = deepClone(obj[key])
            } else {
               result[key] = obj[key]
            }
        }
    }
    return result
}
function deepClone(arr){
    return JSON.parse(JSON.stringify(arr))
}
```
数组乱序
```
function mixin (arr){
    arr.sort(function (){
        return Math.random()-0.5
    })
} 

function shuffle(arr){
    let m = arr.length;
    while(m > 1){
        let index = parseInt(Math.random() * m--);
        [arr[index],arr[m]] = [arr[m],arr[index]];
    }
    return arr;
}
```
数组去重
```
function 
```
实现eventEmitter
```
class EventEmitter {
    constructor(){
        this.events = {}
    }
    on(name,cb){
        if(!this.events[name]){
            this.events[name] = [cb];
        }else{
            this.events[name].push(cb)
        }
    }
    emit(name,...arg){
        if(this.events[name]){
            this.events[name].forEach(fn => {
                fn.call(this,...arg)
            })
        }
    }
    off(name,cb){
        if(this.events[name]){
            this.events[name] = this.events[name].filter(fn => {
                return fn != cb
            })
        }
    }
    once(name,fn){
        var onlyOnce = () => {
            fn.apply(this,arguments);
            this.off(name,onlyOnce)
        }
        this.on(name,onlyOnce);
        return this;
    }
}

```
继承
```
function parent(name) {
    this.name = name
}
parent.prototype.say = function (){
    console.log(this.name)
}
function Child(name,sex){
    parent.call(this, name)
    this.sex = sex
}
Child.prototype = object,create(parent.prototype)
Child.prototype.constructor = Child


class Parent {
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
}

class Child extends Parents{
    constructor(name,age,sex){
        super(name,age);
        this.sex = sex; // 必须先调用super，才能使用this
    }
}
```
instanceof
```
function instanceof(left, right){
    let proto = left.__proto__
    let prototype = right.prototype
    while(true){
        if(proto===null){
            return false
        }
        if(proto === prototype){
            return true
        }
        proto = proto.__proto__
    }
}
```
实现JSONP
```
function handleResponse(response){
    alert("You’re at IP address " + response.ip + ", which is in " +response.city + ", " + response.region_name);    
    }
    var script = document.createElement("script");
    script.src = "http://freegeoip.net/json/?callback=handleResponse";
    document.body.insertBefore(script,document.body.firstChild);    
}

```
实现sleep
```
function sleep(time) {
    return new Promise((resolved, rejected)=>{
        setTimeOut(()=>{
            resloved()
        },time)
    })
}
```
实现promise.all
```
promise.all = function (arr){
    if(!Array.isArray(arr)){
        throw new typeError('is not array')
    }
    let resolveNum = 0;
    let resolveArr = [];
    for(let i = 0;i<arr.length;i++){
        arr[i].then((data)=>{
            resolveNum++;
            resolveArr[i] = data
            if(resolve === arr.length){
                return resolve(resolveArr)
            }
        }).catch(data => {
                return reject(data)
            })
    }
}
```
实现最多并发10个
```
function concurrentPoll(){
    this.task = [];
    this.max = 10;
    setTimeout(()=>{
        this.run()
    },0)
}
concurrentPoll.prototype.addTask = function(task){
    this.task.push(task)
}
concurrentPoll.prototype.run = function(){
    if(this.tasks.length == 0){
        return 
    }
    let length = Math.min(this.max,this.task.length)
    for(let i = 0;i<length;i++){
        this.max--;
        let onetask = this.task.shift()
        onetask().then(()=>{
            console.log(1)
        }).catch(()=>{
            console.log(2)
        })
    }
}
```

[限制并发](https://www.jianshu.com/p/cc706239c7ef)
```
class LimitPromise {
  constructor (max) {
    // 异步任务“并发”上限
    this._max = max
    // 当前正在执行的任务数量
    this._count = 0
    // 等待执行的任务队列
    this._taskQueue = []
  }

  /**
   * 调用器，将异步任务函数和它的参数传入
   * @param caller 异步任务函数，它必须是async函数或者返回Promise的函数
   * @param args 异步任务函数的参数列表
   * @returns {Promise<unknown>} 返回一个新的Promise
   */
  call (caller, ...args) {
    return new Promise((resolve, reject) => {
      const task = this._createTask(caller, args, resolve, reject)
      if (this._count >= this._max) {
        // console.log('count >= max, push a task to queue')
        this._taskQueue.push(task)
      } else {
        task()
      }
    })
  }

  /**
   * 创建一个任务
   * @param caller 实际执行的函数
   * @param args 执行函数的参数
   * @param resolve
   * @param reject
   * @returns {Function} 返回一个任务函数
   * @private
   */
  _createTask (caller, args, resolve, reject) {
    return () => {
      // 实际上是在这里调用了异步任务，并将异步任务的返回（resolve和reject）抛给了上层
      caller(...args)
        .then(resolve)
        .catch(reject)
        .finally(() => {
          // 任务队列的消费区，利用Promise的finally方法，在异步任务结束后，取出下一个任务执行
          this._count--
          if (this._taskQueue.length) {
            // console.log('a task run over, pop a task to run')
            let task = this._taskQueue.shift()
            task()
          } else {
            // console.log('task count = ', count)
          }
        })
      this._count++
      // console.log('task run , task count = ', count)
    }
  }
}
```
二叉树层序遍历
```
function (head){
    if(!head){
        return null
    }
    let res = [];
    let level = 0;
    let queue = head
    while(queue.length !== 0){
        let size = queue.length
        res.push([])
        while(size--){
            let item = queue.shift()
            res[level].push(item.val)
            if(item.left) queue.push(item.left)
            if(item.right) queue.push(item.right)
        }
        levle++
    }
    return res
}
```
二叉树右视图
```
function (head){
    if(!head){
        return null
    }
    let res = [];
    let level = 0;
    let queue = head
    while(queue.length !== 0){
        let size = queue.length
        res.push(queue[0].val)
        while(size--){
            let item = queue.shift()
            if(item.left) queue.push(item.left)
            if(item.right) queue.push(item.right)
        }
        levle++
    }
    return res
}
```
前序遍历
```
funtion preorderTraversal(root) {
    let arr = []
    function tarver(root){
        if(root === null){
            return 
        }
        arr.push(root.val)
        tarver(root.left)
        tarver(root.right)
    }
}
funtion preorderTraversal(root) {
    let queue = [],res = [];
    queue.push(root)
    while(queue.length){
        let item = queue.pop()
        res.push(item.val)
        if(node.right)  queue.push(item.right)
        if(node.left)  queue.push(item.left)
    }
}



funtion preorderTraversal(root) {
    let arr = []
    function tarver(root){
        if(root === null){
            return 
        }
        tarver(root.left)
        arr.push(root.val)
        tarver(root.right)
    }
}
funtion preorderTraversal(root) {
    let arr = []
    function tarver(root){
        if(root === null){
            return 
        }
        tarver(root.left)
        tarver(root.right)
         arr.push(root.val)
    }
}
```

二叉树深度计算
```
最大深度
function finddeep(root){
    if(root === null) return 0
    return Math.max(finddeep(root.left)+1, finddeep(root.right)+1)
}

function deep(root){
    let queue = [];
    let res = [];
    let level = 0;
    queue.push(root)
    while(queue.length){
        res.push([])
        let size = queue.length
        whilr(size--){
            let item = queue.shift()
            if(item.left) res[level].push(item.left)
            if(item.right) res[level].push(item.right)
        }
        level++
    }
    return level
}

最小深度
function mindeep(root){
    if(root === null) return 0
    if(root.left)
}
```
镜像二叉树判断
```
function isSame(root){
    istwoSame(root, root)
}
function istwoSame(left, right){
    if(!left && !right){
        return true
    }
    if(!left || !right){
        return false
    }
    if(left.val !== right.val){
        return false
    }
    return istwoSame(left.left, left.right) && istwoSame(right.left, right.right)
}
```