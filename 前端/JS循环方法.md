[for-in+for-of+forEach区别](https://blog.fundebug.com/2019/03/11/4-ways-to-loop-array-inj-javascript/)

# for-in

遍历数组索引、对象、String的可枚举属性（包括自有属性、原型链上的属性）, 取出的是key

- 不一定按特定顺序返回数组索引，遍历得到的索引是字符串。所以一般不用做数组

- 可手动中断或跳出

- 保留外部作用域的this

- 跳过空数组（console.log  ["a", , "c"]=> a c）

- 数组，不会忽略非数字属性

  ```javascript
  const arr = ["a", "b", "c"];
  arr.test = "bad";
  
  for (let i in arr) {
      console.log(arr[i]); // 打印"a, b, c, bad"
  }
  ```

  



# forEach

遍历包括原型链上的可枚举属性

```arr.forEach(function(value, index, arr){}, [thisArg])```

- 跳过空数组



# for-of

遍历 Array、String、Map、Set、Arguments对象等可迭代的数据结构，取出的是item

- 可手动中断或跳出

- 不能遍历Object对象
- 按序迭代数组
- 不跳过空数组，得到undefined



# map()

遍历数组，对数组中每一项做改造，返回新数组，不改变原数组

```let newArr = arr.map(function(value, index, arr){}, [thisArg])```

- return



# filter

遍历，过滤出数组中符合条件的数组，组成新数组，不会改变原数组

```let newArr = arr.filter(function(value, index, arr){return value > 10}, [thisArg])```

- return



# every()

遍历数组，看其每一项是否全满足条件，全满足返回true，不会改变原数组

```let falg = arr.every(function(value, index, arr){return value > 10}, [thisArg])```



# some()

遍历数组，只要其中一项满足条件即可，返回true，不会改变原数组

```let falg = arr.some(function(value, index, arr){return value > 10}, [thisArg])```



# Object.getOwnProperty

返回所有自有的可枚举、不可枚举属性

- 数组形式



# Object.keys

返回自有的可枚举属性

- 数组形式



# Array.prototype.keys





# Object.entries

返回自有的可枚举属性及其值

- 二维数组，键值对 [[name, 'Qiyao'],[age: 21]]



# Array.prototype.entries