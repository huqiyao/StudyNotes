# 实战记录

## 一些小问题

1. 为什么执行后出现  ```undefined```

   > 因为**每执行一次代码，就会返回该表达式的返回值**。console.log()，var a = xx等这些并没有返回值，所以undefined

   <div align="center"><img src="..\图片资料\printUndefinedPic.png" height="200px;" width="500px;"/></div>



## 异步编程



### 补充：JavaScript运行机制

#### 解释单线程和异步

JavaScript语言本身是单线程执行的，但是其宿主环境是多线程的，通过事件驱动使js表现出异步

#### 主线程和任务队列

同步任务执行完后才会执行异步任务









### 回调函数基本介绍

1. 回调函数格式：

   > **function(err,results,……)**：一般是两个参数，可能有的会有更多
   >
   > - err表示操作的成功或失败状态，其值：
   >
   >   :one: null：表示操作成功
   >
   >   :two: 一个Error对象的实例 
   >
   > - results表示操作返回的的结果或信息(文件句柄、数据库连接、查询到的数据集等)

2. 问：什么时候要用到回调函数？

   > ==**答**==：不需要立刻获得读取的结果，且除了读取这件事下面还有其他代码需要执行

3. 问：什么时候再回来执行回调函数？

  > **==答==**：  返回结果时会通知回调函数（普通函数由所写代码调用，回调函数由操作系统合适时间调用）
  >
  > ```mermaid
  > graph LR
  > A[检查验证参数] -->B[通知Node核心排队执行函数]
  > B-->C{func A}
  > C-.等待结果.->F[返回结果]
  > F-.通知.->G[调用回调函数]
  > C--继续执行-->D{......}
  > D--继续执行-->E{func ...}
  > 
  > 
  > ```





  ### ```读取文件内容demo:```

 <div align='left'><img src='..\图片资料\readFileProcess.png'/>
    </div>

 <div align='left'><img src='..\图片资料\wrongReadFileProcess.png'/>
    </div>






### 回调函数与异常处理

- **setTimeout函数在Node的事件队列中添加了新事件**(告诉node1000ms后调用)，该回调函数是**在全新的上下文和作用域中执行的**。

  ```javascript
  var num = undefined
  // 与异步编程有关
  try {
  // 回调函数执行时，try...catch已经执行过了
    setTimeout(function () {
        console.log(num.toString())
    }, 1000) 
  } catch (e) {
    console.log("error……" + e.message)
  }
  // 与异步编程无关，肯定会出错
  try 
    var demo = function () {
        console.log(num.toString())
    }
  } catch (e) {
  // 不会捕捉到错误因为var demo = xxx的赋值没错,
    console.log("error……" + e.message) 
  }
  // 该函数执行时内部才会报错
  demo() 
  ```
  



### 规范的错误处理

- 第一种

  ``` javascript
  function(err,handle){
      if(err){
          console.log("ERROR: " + err.code + "(" + err.message + ")");
          return;
      }
      ……
  }
  ```



- 第二种

  ```javascript
  function(err,handle){
      if(err){
          console.log("ERROR: " + err.code + "(" + err.message + ")");
      }
      else{
          ……
      }
  }
  ```

  



 ### 维护本体

<div align='center'><img src='..\图片资料\fileCallback.png'></div> 

- 为什么是打开失败时，fileName是undefined的

  > ```mermaid
  > graph TB
  > A[fs.open函数初始化本身]-->B[调用底层操作系统函数来打开文件]
  > B-->C[将回调函数插入到事件队列中]
  > 
  > ```
  >
  > 