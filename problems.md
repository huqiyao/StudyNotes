## this在node环境中

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




## Window 和 window

