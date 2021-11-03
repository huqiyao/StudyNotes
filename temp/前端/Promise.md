Promise 是异步编程的一种解决方案，比传统的异步解决方案【回调函数】和【事件】更合理、更强大。现已被 ES6 纳入进规范中

# Promise面试题

## Promise 解决的痛点是什么？

> 解决了回调地狱的问题。





## Promise 的业界实现都有哪些？

> Q 、bluebird





## Promise 如何使用？

- 初始化一个Promise对象。可以通过 ```new Promise(fn)``` 或 ```Promise.resolve(fn)``` 方法
- 



## Promise 常用的方法有哪些？它们的作用是什么

- catch，捕获前面的回调产生的错误的结果，并处理
- then，为上一个异步操作返回的Promise对象或结果注册回调函数
- race，使得多个异步任务同时进行，哪个任务最先执行完即返回其结果
- all，使得多个异步任务同时进行，等所有任务都执行完才返回所有结果，如果有一个rejected了，就只返回这个rejected的结果
- resolve，返回一个以 value 值解析后的 Promise 对象
  - 如果 value 是 thenable，返回一个状态跟 thenable一样的Promise对象
  - 如果 value 是 Promise对象，返回这个Promise对象
  - 如果 value是其他值，以 value 值为成功状态返回一个Promise对象
- reject，同上，只是状态不同





# Promise源码

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

  