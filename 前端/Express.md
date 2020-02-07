# 路由

- 路由函数：```app.method(url, optional_method, function(req,res,next){})```



# 新建项目





# 设置静态资源目录

> **静态资源：**内容不会变化，不同用户看到的内容都是一样的

> **设置的目的：**将该目录下的文件设置为浏览器可访问的，即用户可以看到的。
>
> 如输入：``` http://localhost:3000/images/bg.png ```

> ``` app.use ([paht,] function [, function ...] )  ```：相当于消息中间件，用来注册中间件函数。所有```[paht,]```请求先交给```function```处理



## 方法

```javascript
// 指定静态资源目录
app.use(express.static(__dirname + "/public"));

app.use(express.static(path.join(__dirname,'public' )))

// 可以使用虚拟静态资源目录
app.use('/static', express.static (__dirname + "/public")); // 所以 /static 就代表了 __dirname/public

// 在当前项目文件夹下启动项目还可以用：
app.use('/static', express.static ("/public"));
```







