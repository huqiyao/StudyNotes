# this在node环境中

> **node环境：**
>
> 在全局环境中，this指的是 ```module.exports``` 对象
>
> - 但在node控制台中，this指的就是Global对象
>
> 全局调用函数时，this指的是Global对象
>
> **浏览器环境：**
>
> 两种情况指的都是Window对象

```javascript
function fun(){
    this.name = 'Qiyao';
    console.log(this);
}
fun(); // 打印的this是Global对象，(见下图)
console.log(this); // {}，这个this是module.exports对象
this.age = 21;
console.log(this); // {age:21}
```

<div align='center'><img src='图片资料/node中的this.png'></div>


# Window 和 window 





# substring 和 substr

- substr(start [, length])
  - length 为0或者负数，返回空字符串
- substring(start [, end])
  - 使用start、end中的较小值作为起始点
  - start 或 end 为 NaN / 负数时，将其替换成 0



# console.log() 和 console.dir()

```javascript
function Foo(){
    console.log(1)
}
```

- 如果是```console.log(Foo)```

  <div text-align='center'><img src='./图片资料/log结果.png'></div>

- 如果是```console.dir(Foo)```

  <div text-align='center'><img src='./图片资料/dir结果.png'></div>



# 输错一次用户名和密码，就没有重输的机会，一直Authentication failed

[参考资料](https://blog.csdn.net/qq_34665539/article/details/80408282)

打开 windows 的凭据管理器，删除上次输错的记录



# 关于基本类型与构造函数实例的问题

```javascript
var str = "hello world";
console.log(str instanceof String); // false
console.log(str.__proto__ === String.prototype); // true
```



# 判空的问题

```javascript
var tags = []
console.log(tags === []) // 为什么返回false
```



# toString 与 toString()



# function的name

```javascript
// 为function及function的prototype增加name属性，并赋值
function Foo(){
    console.log(1)
}
Foo.name = 'Atong'
Foo.prototype.name = 'Qiyao'
console.dir(Foo)
```

<div text-align='center'><img src='./图片资料/problems-function的name_1.png'></div>

```javascript
// 为function及function的prototype增加nickname属性，并赋值
function Foo(){
    console.log(1)
}
Foo.nickname = 'Atong'
Foo.prototype.nickname = 'Qiyao'
console.dir(Foo)
```

<div text-align='center'><img src='./图片资料/problems-function的name_2.png'></div>

> 综上：这个是非匿名函数，自身有个内置属性```name = 函数名``` , 是不会被修改的
>
> 即使是匿名函数，也有内置属性name，只是```name = ''```，也是不能被修改的



# 使用iView的Col、Input标签报错

https://blog.csdn.net/weixin_38465623/article/details/85490353

https://blog.csdn.net/jiaqingge/article/details/80498536



# 管理员查看不到我的feature分支

https://www.cnblogs.com/zhou-chao/p/7678899.html