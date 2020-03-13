## Arguments

- arguments是所有(非箭头)函数内部都可访问到的一个类数组对象，保存有函数的参数列表



## 转换为真数组

```slice```  源码：

```javascript
Array.prototype.slice = function(start, end){
    var result = new Array()
    start = start || 0
    end = end || this.length
    for(var i = start; i < end; i++){
        result.push(this[i])
    }
    return result
}
```

所以  ```slice.call(arguments,num1,num2)```  转换```arguments``` 数组对象为数组的原理是：

> 将 ```slice```  的 ```this```  指向arguments，num1、num2作为可选的参数，分别代表start和end



- ```js
  Array.prototype.slice.call(arguments,num1,num2)
  ```



- ```javascript
  Array.from(arguments)
  ```




- ```javascript
  [].slice.call(arguments)
  ```

  