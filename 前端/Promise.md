Promise 是异步编程的一种解决方案，比传统的异步解决方案【回调函数】和【事件】更合理、更强大。现已被 ES6 纳入进规范中



## Promise 解决的痛点是什么？

> 解决了回调地狱的问题。





## Promise 的业界实现都有哪些？

> Q 、bluebird





## Promise 如何使用？

> - 初始化一个Promise对象。可以通过 ```new Promise(fn)``` 或 ```Promise.resolve(fn)``` 方法





## Promise源码

```javascript
const PENDING = 'pending';
const RESOLVED = 'resolved';
const REJECTED = 'rejected';
function Promise = (executor){
    let self = this;
    self.onFulfiled = [];
    self.onRejected = [];
    self.status = PENDING;
    self.value = undefined;
    self.reason = undefined;
    function resolve(value){
        if(self.status == PENDING){
            self.status = RESOLVED;
            self.value = value;
            self.onFulfiled.forEach(fn=>fn())
        }
    }
    function 
}
```

