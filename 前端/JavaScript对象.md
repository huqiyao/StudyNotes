# 创建对象

[参考资料]( https://juejin.im/entry/58291447128fe1005cd41c52#comment )

## √对象字面量方法

```javascript
var person1 = {
    name: "Wang",
    age: 11,
    sayName: function(){
        console.log(this.name);
    }
}
```





## √工厂模式

```javascript
function createPerson(name, age){
    var o = new Object();
    o.age = age;
    o.name = name;
    o.sayName = function(){
        console.log(this.name);
    }
}
var person1 = createPerson("Wang",11);
```

- 无法通过constructor识别具体对象，只知道Object而不知是Person



## √构造函数模式

- 除了Object、Array等原生构造函数，还可以自定义构造函数

```javascript
function Person(name, age){
    this.name = name;
    this.age = age;
    this.sayName = function(){ // 相当于new Function("console.log('this.name')")
        console.log(this.name);
    }
}
var person1 = new Person("Wang",11); // new的方式调用构造函数创建实例
```

-  通过constructor或者instanceof可以识别对象实例的类别 
- 对象的每个方法都要在不同实例上重新创建一遍



### 调用构造函数实例化过程

- 创建新对象
- 将构造函数的作用域赋给新对象 (this指向新对象)
- 执行构造函数中的代码 (给新对象添加属性)
- 返回新对象





## √原型模式

```javascript
function Person(){};
Person.prototype.name = "Wang";
Person.prototype.age = 11;
Person.prototype.sayName = function(){
    console.log(this.name);
}
// 简化写法
Person.prototype = {
    name:"Wang",
    age: 11,
    sayName:function(){
        console.log(this.name);
    }
}
var person1 = new Person();
```





## √组合构造函数模式与原型模式

```javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype = {
    constructor: Person,
    sayName: function(){
        console.log(this.name);
    }
}
var person = new Person("Wang", 11);
```





## 动态原型模式



## 寄生构造函数模型

```javascript
function Person(name, age){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.sayName = function(){
        console.log(this.name);
    }
}
```



## 稳妥构造函数模式

