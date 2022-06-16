## 杂记



1. 特点：

   - 强大的类型系统降低了模块阅读和使用成本

   - 编译期进行静态类型分析，避免在运行时报错
   - 加入基于Class的对象、接口、模块，给大型项目提供构建机制，有利于扩展和维护



2. 开启 ```--noImplicitReturns``` 参数后，下述代码编译失败

```typescript
getOne(_id: string):string {
  const result = cacheService.exist(_id)
  if(result) {
    return cacheService.findByid(_id)
  }
}
```



3. 以代码中模块的数量和模块之间的依赖关系来评判应用的规模。将大规模的应用定义为，需要众多开发者一同维护且具有一定复杂度的程序。



4. TypeScript 是 JavaScript 的超集，任何合法的 JavaScript 程序都是合法的 TypeScript 程序



5. 