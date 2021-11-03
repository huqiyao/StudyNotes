# 简介

symbol 是 ES6 新增的基本数据类型，用来生成一个全局唯一的值；

可以理解为，它是一种类似于字符串的数据类型



# 特点

- Symbol 函数前面不能有 ```new``` 命令

- 可以接收字符串作为参数（如果是其他类型的参数，会调用toString方法转成string），这个参数只是个名字，不影响值。

  实质是 ```Symbol.prototype.description```，可通过 ```sym.description``` 获得

  - ```javascript
    var sym = Symbol(null); // Symbol(null)
    var sym = Symbol(undefined); // Symbol()
    var sym = Symbol(123); // Symbol(123)
    var sym = Symbol(Symbol(12)); // TypeError: Cannot convert a Symbol value to a string，因为不能隐式转换咯
    ```

- symbol 类型的值，可以**显式**转为字符串( ```toString``` , ```String()``` )、布尔值( ```Boolan()``` )，不能转为数值(```Number()```)

- Symbol 类型的值，不能与其他值进行计算，会报错```TypeError: Cannot convert a Symbol value to a string```

  - ```javascript
    var sym = Symbol("demo");
    `your symbol is ${sym}` // ×
    ```

    

# 场景

[使用场景](https://www.jianshu.com/p/f40a77bbd74e)

- 作为对象的属性名 [封装私有属性](https://juejin.im/post/5c7e14fff265da2dd77403af#comment)

  - Symbol作为属性，不能使用```for...in```、 ```for...of``` 遍历，

    不存在于```Object.keys()```、 ```Object.getOwnPropertyNames()``` 获得的属性中，

    将对象通过```JSON.stringfy()``` 转为JSON字符串后，属性也不存在其中

  - 但可以通过 ```Object.getOwnPropertySymbols()``` 、```Reflect.ownKeys()``` 获得

  - 虽然不能作为真正的私有属性，但是可以分离对象的公共和内部属性

    ```javascript
    var Pet = (function() {
      function Pet(type) {
        this.type = type;
      }
      Pet.prototype.getType = function() {
        return this.type;
      }
      return Pet;
    }());
    
    var a = new Pet('dog');
    console.log(a.getType());//Output: dog
    a.type = null;//Modified outside
    console.log(a.getType());//Output: null
    
    // 使用Symbol
    var Pet = (function() {
      var typeSymbol = Symbol('type');
      function Pet(type) {
        this[typeSymbol] = type;
      }
      Pet.prototype.getType = function(){
        return this[typeSymbol];
      }
      return Pet;
    }());
    var a = new Pet('dog');
    console.log(a.getType());//Output: dog
    a.type = null;//Stays private
    console.log(a.getType());//Output: dog
    ```

    

- 替代常量

  ```javascript
  const TYPE_AUDIO = 'AUDIO'
  const TYPE_VIDEO = 'VIDEO'
  const TYPE_IMAGE = 'IMAGE'
  
  function handleFileResource(resource) {
    switch(resource.type) {
      case TYPE_AUDIO:
        playAudio(resource)
        break
      case TYPE_VIDEO:
        playVideo(resource)
        break
      case TYPE_IMAGE:
        previewImage(resource)
        break
      default:
        throw new Error('Unknown type of resource')
    }
  }
  ```



- 注册和获取全局Symbol

  应用涉及多个window时 (比如iframe)

  ```javascript
  // 使用Symbol.for API，使得不同窗口中属性名都唯一，且能访问到
  let gs1 = Symbol.for('global_symbol_1')  //注册一个全局Symbol
  let gs2 = Symbol.for('global_symbol_1')  //获取全局Symbol
  
  gs1 === gs2  // true
  ```

  