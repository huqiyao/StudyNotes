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





## substring 和 substr

- substr(start [, length])
  - length 为0或者负数，返回空字符串
- substring(start [, end])
  - 使用start、end中的较小值作为起始点
  - start 或 end 为 NaN / 负数时，将其替换成 0



## console.log() 和 console.dir()

