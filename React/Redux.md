# createSelector



## 使用



> **reselect**（redux的中间件）的一个方法

[参考资料](https://www.tangshuang.net/3839.html)

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

f3是个纯函数

如果f3实参不变（即fun1、fun2结果都不变），则f3返回与上次相同的值，即缓存；否则返回重新计算后的结果



### 实现原理

