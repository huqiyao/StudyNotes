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
            self.onFulfiled.forEach(fn=>fn(self.value));
        }
    }
    function reject(reason){
        if(self.status == PENDING){
            self.status = REJECTED;
            self.reason = reason;
            self.onRejected.forEach(fn=>fn(self.reason));
        }
    }
    try{
        executor(resolve,reject);
    }catch(e){
        reject(e);
    }
}

// 原型方法 then
Promise.prototype.then = function(onFulfiled, onRejected){
    onFulfiled = typeof onFulfiled == 'function' ? onFulfiled : value => value;
    onRejected = typeof onRejected == 'function' ? onRejected : reason => {throw reason};
    let self = this;
    let promise2 = new Promise((resolve, reject)=>{
        if(self.status == RESOLVED){
            setTimeOut(()=>{
                try{
                	let x = onFulfiled(self.value);
                    resolvePromise(x,promise2,resolve,reject); // 这个方法不会
            	}catch(e){
                	reject(e);
            	}
            });
        }else if(self.status == REJECTED){
            setTimeOut(()=>{
                try{
                	let x = onRejected(self.reason);
                    resolvePromise(x,promise2,resolve,reject);
            	}catch(e){
                	reject(e);
            	}
            });
        }else if(self.status == PENDING){
            self.onFulfiled.push(setTimeOut(()=>{
                try{
                    let x = onFulfiled(self.value);
                    resolvePromise(x,promise2,resolve,reject);
                }catch(e){
                    reject(e);
                }
            }));
            self.onRejected.push(setTimeOut(()=>{
                try{
                    let x = onRejected(self.value);
                    resolvePromise(x,promise2,resolve,reject);
                }catch(e){
                    reject(e);
                }
            }));
        }
    });
    return promise2;
}
```

- 原型方法：```catch```	```then```	```finally```

- 属性方法：```all```	```race```	```reject```	```resolve```

  