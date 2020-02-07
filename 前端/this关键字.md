# 方法 与 this 
[参考资料:The this keyword]( https://www.quirksmode.org/js/this.html )

## copy

> func方法的副本，成了元素element的onclick属性的值
>
> ```javascript
> function func(){
>     this.style.color = '#cc0000';
> }
> element.onclick = func;
> /**
> * 检验
> */
> console.log(element.onclick); // function func(){ this.style.color = '#cc0000'}
> ```

- ```element.onclick = func;```

- ```element.addEventListener('click', func, false);```

- ```element.onclick = function(){ this.style.color = '#cc0000'; }```

- ```<element onclick = "this.style.color = '#cc0000';" >```

- :star:```<element onclick="func(this)">  function func(obj){ obj.style.color = '#cc0000'; }```

  

## refer

> 元素element的onclick属性，是func函数的调用  （tell: go to func and execute）
>
> 所以this指向的内容不是元素element, 是window对象 （但window对象没有style属性，所以报错）

- ```element.onclick = function() { func() }```

- ```element.attachEvent('onclick', func)```
- ```<element onclick="func()">```





# this 与 箭头函数

