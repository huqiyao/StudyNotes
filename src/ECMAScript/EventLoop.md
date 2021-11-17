# EventLoop

* [宏任务](#宏任务)
* [微任务](#微任务)



> Todos:
>
> 1. 宏任务、微任务、同步任务、异步任务
>
> 2. 回调函数是什么时候进入EventQueue的，EventTable又是个什么机制
>
> 3. ajax请求、settimeout的timer是在哪里执行的呢
>
> 4. js引擎怎么知道哪些是异步、哪些是同步任务呢
>
>    > 这就是js引擎自己定义的，怎么会不知道呢
>    
> 5. [为什么要区分宏任务、微任务呢](https://www.zhihu.com/question/316514618)
>
> 6. 🤔️ Promise的then的回调函数是什么时候进入微任务队列的？




## 宏任务

script(整体代码)
setTimeout
setInterval
I/O
UI交互事件
postMessage
MessageChannel
setImmediate(Node.js 环境)



## 微任务

Promise.then
Object.observe
MutationObserver
process.nextTick(Node.js 环境)



## 引用

- [1] [then的回调什么时候进入任务队列](https://segmentfault.com/q/1010000022578087)
- [2] [简单易懂的EventLoop](https://juejin.cn/post/6844903512845860872)
- [3] [执行栈图解](https://siddharthac6.medium.com/javascript-execution-of-synchronous-and-asynchronous-codes-40f3a199e687)
- [4] [图解EventLoop](https://juejin.cn/post/6844904004745592846)

- [5] [await到底做了什么](https://segmentfault.com/q/1010000016147496)

