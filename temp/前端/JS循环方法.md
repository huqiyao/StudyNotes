[for-in+for-of+forEach区别](https://blog.fundebug.com/2019/03/11/4-ways-to-loop-array-inj-javascript/)

都不会改变原对象

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
      console.log(arr[i]); // 打印'0', '1', '2', 'test'
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

```javascript
const oldArray = [1, 4, 9, 16];

function ourFunc(val, index, arr){
  return val * this.windowSize
}

const newArray = oldArray.map(ourFunc, {windowSize: 10}); // 第2个参数代表callback里的this
```





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



# Object.getOwnPropertyNames

返回所有对象自有的可枚举、不可枚举属性（不包括Symbol值作为名称的属性）

- 字符串数组形式

```javascript
var obj = {name:'qiyao', age:21}
console.log(Object.getOwnProperty(obj)); // ['name', 'age']

var arr = ['a','b','c']
console.log(Object.getOwnProperty(arr)); // ['0','1','2','length']
```





# Object.keys

返回自有的可枚举属性

- 字符串数组形式

```javascript
var arr = ['a','b','c']
console.log(Object.getOwnProperty(arr)); // ['0','1','2']
```





## Array.prototype.keys

返回数组可枚举属性的迭代器

```javascript
var arr = ['a', 'b', 'c', 'd', 'e'];
var iterator = arr.values();

for (let letter of iterator) {
  console.log(letter);
}  //"a" "b" "c" "d" "e"
```







# Object.values()

返回自有的可枚举属性的值

- 字符串数组形式





## Array.prototype.values()

返回数组可枚举属性的值的迭代器





# Object.entries

返回自有的可枚举属性及其值

- 二维数组，键值对 [[name, 'Qiyao'],[age: 21]]





## Array.prototype.entries

返回数组可枚举属性与其值的迭代器

```javascript
var arr = ['a', 'b', 'c']
var iterator = arr.entries();

// ========================
for(let i of iterator){
  console.log(i); // [0,'a'] [1,'b'] [2,'c']
}

// =========================
var item = iterator.next()
item.value // [0, 'a']
item.done // false

var item = iterator.next()
item.value // [1, 'b']
item.done // false

var item = iterator.next()
item.value // [2, 'c']
item.done // false

var item = iterator.next()
item.value // undefined
item.done // true
```

