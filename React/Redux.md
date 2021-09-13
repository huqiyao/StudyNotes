# Flux





# Redux



## 三个原则

### 唯一数据源

项目只有一个store来管理数据，避免了数据不一致、store依赖等问题

store上的数据是树形结构，它的设计是个核心问题，每个组件只用到这棵树的部分数据

一个隐含要求：避免数据冗余，如sum=first + second，那就没必要存储sum了



### 保持状态只读

view只能获取store的值，无法直接修改store存储的数据，只能通过派发一个action对象完成



### 数据改变只能通过纯函数（reducer）完成

flux的register过程直接修改原state的值，而redux返回新的state

```javascript
const arr = [1,2,3]
const reducer = (accumulator, currValue)=> { return xx }
arr.reduce(reducer);
```

redux的reducer函数原理就是js数组reduce方法的reducer回调函数

const reducer = (state = initState, action)=>{ ......return newSate }





# createSelector



## 使用



> **reselect**（redux的中间件）的一个方法，主要功能是缓存数据



[参考资料](https://www.tangshuang.net/3839.html)

[简单易懂](https://juejin.cn/post/6844903866354532365)



```typescript
// 使用范例
const exampleState = {
  shop: {
    taxPercent: 8,
    items: [
      { name: 'apple', value: 1.20 },
      { name: 'orange', value: 0.95 },
    ]
  }
}

const shopItemsSelector = state => state.shop.items // small selector

const subtotalSelector = createSelector( 
  shopItemsSelector,
  items => items.reduce((subtotal, item) => subtotal + item.value, 0)
)

console.log(subtotalSelector(exampleState)) // 2.15
// create出来的selector（subtotalSelector）调用时传入的state参数是 createSelector前n-1个selector函数（shopItemsSelector）所需的state参数
// 其实是（state, props）
```

state是store里的数据？



## 解析



```typescript
const selector = createSelector(fun1, fun2, f3)
// 经过createSelector处理，生成的selector：
(state?, props?)=>{
  const param1 = fun1(state, props);
  const param2 = fun2(state, props);
  return f3(param1, param2)
}
```



## 记忆功能



### 缓存规则

createSelector创建的selector的**记忆规则**：

如果f3实参都不变（即fun1、fun2结果不变），则f3返回与上次相同的值，即缓存；否则返回重新计算后的结果



### 实现原理

state或者props变化，会导致fun1、fun2产生的实参变化，如何实现缓存？









