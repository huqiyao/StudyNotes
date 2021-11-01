# async/await

* [async](#async)
* [await](#await)
* [使用场景](#使用场景)

- [引用](#引用)

<br/><br/>
## async
<br/>
- :wrench:&nbsp;<u>作用</u>：async 将后面的值或者函数包裹成 Promise 对象
- :question:&nbsp;<u>问题</u>：
  - 为什么 await 需要在 async 中使用？
- :boom:&nbsp;<u>caution</u>：
  - 如果不需要async 包裹函数的返回值，那这个函数大多数只是为了作为 await 的载体，调用时就和普通函数一样，不要纠结 async
  - 如果需要得到async包裹函数的返回值，要用then来接收
  <br/><br/>




## await
<br/>

- :wrench:&nbsp;<u>作用</u>：等待一个 Promise 或者一个值

- :+1:&nbsp;<u>优点</u>：同步的写法避免了多个 Promise 情况下形成很长的 then 调用

- :question:&nbsp;<u>问题</u>：
  - 如果 await 等待的 Promise 结果是一个 rejected 怎么捕获错误？所以需要有错误处理
  
    ```javascript
    // 写法一
    async function handle(){
      try{
        await getSomeThing()
      }catch(err){
        console.log('err',err)
      }
    }
    // 写法二
    async function handle(){
      await getSomeThing().catch(err=>{
        console.log(err)
      })
    }
    ```
  
  - 如果等待的Promise的结果还是一个Promise ```resolve(new Promise(()=>{...}))```，怎么处理？
  
    ```javascript
    ```
  
    
  


 <br/><br/>  



## 使用场景





## 引用

- [1] [segmentfault资料](https://segmentfault.com/a/1190000007535316)

