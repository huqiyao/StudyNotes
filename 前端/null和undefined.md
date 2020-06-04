# null

- 意味着 空的 或者 不存在的值

  - 比如获取一个不存在的节点 ```document.getElementById('notExistElement')```

- ``` javascript
  var num = null; console.log(typeof num); // object 
  // 是最初实现JavaScript的错误，现在被解释为：一个不存在的对象的占位符
  ```



# undefined

- 意味着变量被申明了，但是值没有被定义

  - ```javascript
    // but
    var obj = {};
    console.log(obj.props); // undefined
    ```

- ```javascript
  var num = undefined; console.log(typeof num); // undefined
  ```

  

# undefined == null

# undefined !== null



