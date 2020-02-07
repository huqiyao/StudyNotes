## ```put```  ```post```  ```patch```

[put/post区别1](https://stackoverflow.com/questions/31089221/what-is-the-difference-between-put-post-and-patch)

[put/post区别2](https://stackoverflow.com/questions/630453/put-vs-post-in-rest/630475#2590281)

### ```put```

- 新建/更改资源

- 新建资源时(create)，客户端来指定资源名称
- 幂等操作

```javascript
// 新建
PUT /questions/<new_question>
// 修改
PUT /questions/<existing_question>
```



### ```post```

- 新建/更改资源

- 新建资源时(create)，服务器来指定资源名称
- 非幂等操作

```javascript
// 新建
POST /questions/
// 修改
POST /questions/<existing_question>
```



### ```patch```

[什么时候用patch](https://segmentfault.com/q/1010000005685904)

- 更改局部资源
- 非幂等操作

