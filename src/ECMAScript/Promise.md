# Promise

- [介绍](#介绍)

* [Promise实例的方法](#Promise实例的方法)
  * [then](#then)
  * [catch](#catch)
  * [finally](#finally)
  * [all](#all)
  * [race](#race)

- [引用](#引用)



## 介绍

- :question:&nbsp;Promise对象是什么

  > 一个 Promise 相当于保存着异步事件结果的容器

- :question:

  > 如果改变已经发生了，你再对`Promise`对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。



### Promise对象的状态

- pending
- fulfiled
- rejected

resolve另一promise实例。`p1`的状态就会传递给`p2`，也就是说，`p1`的状态决定了`p2`的状态。如果`p1`的状态是`pending`，那么`p2`的回调函数就会等待`p1`的状态改变；如果`p1`的状态已经是`resolved`或者`rejected`，那么`p2`的回调函数将会立刻执行。



写在resolve、reject他们之后的语句会执行的；且如果是同步任务会优先于他们执行。一般来说，调用`resolve`或`reject`以后，Promise 的使命就完成了，后继操作应该放到`then`方法里面，而不应该直接写在`resolve`或`reject`的后面。所以，最好在它们前面加上`return`语句，这样就不会有意外。



## Promise实例的方法



### then

`then`方法返回的是一个新的`Promise`实例（注意，不是原来那个`Promise`实例）。因此可以采用链式写法，即`then`方法后面再调用另一个`then`方法。

:question:&nbsp;怎么返回一个新promise的？

:question:&nbsp;如果then中只是console.log了一下呢。这个promise对象长啥样，后续的then怎么接？



then 中新创建的 Promise，它的状态变为 fulfilled 的节点是在上一个 Promise的回调执行完毕的时候。

前一个回调函数，有可能返回的还是一个`Promise`对象（即有异步操作），这时后一个回调函数，就会等待该`Promise`对象的状态发生变化，才会被调用。



### catch

- catch
  - 和then的第二个参数一样，用来指定reject的回调。但是
  - 在执行resolve的回调（也就是上面then中的第一个参数）时，如果抛出异常了（代码出错了），那么并不会报错卡死js，而是会进到这个catch方法中
  - 两个参数(resolved的回调函数、rejected的回调函数)都是可选的



## 过程



## 原理



## 引用

- [1] [掘金资料1](https://juejin.cn/post/6844903607968481287)

- [2] [掘金资料2](https://juejin.cn/post/6844904063570542599)

- [3] [阮一峰ES6](https://es6.ruanyifeng.com/#docs/promise)

- [4] [MDN-Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

