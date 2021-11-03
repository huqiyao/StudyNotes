## 实现map方法

```javascript
if(Array.prototype.newMap == undefined){
    Array.prototype.newMap = function(fn){
        var rv = [];
        for(var i = 0; i < this.length; i++){
            rv.push(fn(this[i]));
        }
        return rv;
    }
}
// 使用
var arr = [1,2,3];
var res = arr.newMap(function(item){
    console.log(item); 
    // 1
    // 2
    // 3
    console.log(this);
    // Global Object
    // Global Object
    // Global Object
    return item*item;
})
console.log(res); // [1,4,9]
```



## 思考

### 回调函数作为参数

- 函数A定义，括号里的参数是一个回调函数时，只需要写函数名。至于回调函数的参数是什么由该函数A定义过程中决定。

  实际调用时，随便取个名字即可



### 回调函数的this

- 由上面 ```newMap``` 中调用回调函数可知，没有 ```object.fn()``` ，因为没有调用对象，所以this指的就是全局对象



