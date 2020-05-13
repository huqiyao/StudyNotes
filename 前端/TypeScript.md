# 简介

## 特点

- 静态类型检测 的 弱类型语言	[见评论第一条](https://www.zhihu.com/question/19918532)

- 具有类型系统

- 是js的超集，兼容了js的所有语法，又增加了新的特性

- 自带了完备的Language Service，包括但不限于自动补全、错误提示等功能，提高生产力  [一些误区](https://www.jianshu.com/p/d2d15111f9d4)

- 编译阶段报错，也还会生成js文件 (报错不想生成js，可在```tsconfig.json``` 里配置 ```noEmitOnError```)

  

# 数据类型

## 基本类型



### JS原始类型

- boolean

  ```typescript
  let isDone : boolean = false;
  // ==========================
  // 使用构造函数 Boolean 创造的不是布尔值，而是Boolean对象；直接调用 Boolean，创造的是布尔值
  // 其他的基本类型的构造函数同理(String,Number,)
  let isDone : Boolean = new Boolean(true);
  ```

  

- number

  ```typescript
  let decLiteral: number = 6;
  let hexLiteral: number = 0xf00d; // 不变，不会被编译成十进制
  let binaryLiteral: number = 0b1010;//二进制被编译为十进制
  let octalLiteral: number = 0o744;//八进制被编译为十进制
  let notANumber: number = NaN;
  let infinityNumber: number = Infinity;
  ```



- string

  ```typescript
  let name: string = 'Tom';
  let age: number = 21;
  // 模板字符串
  let sentence: string = `My name is ${myName}.
  I am ${myAge + 1} years old`;
  // 编译结果：
  var sentence = "My name is" + myName + "\n.I am" +(myAge + 1) + "years old";
  ```

  

- null 与 undefined  <a src="./null和undefined.md">undefined和null</a>

  一般用来为变量赋初值
  
  null、undefined 是所有类型（除了never）的子类型，所以null、undefined类型的值可以赋值给任何类型（除了never）的变量
  
  ```typescript
  let num : null = null;
  ```
  
  ```typescript
  let num : undefined = undefined;
  // =============================
  let a : undefined;
  let b : number = a;
  // 相当于：var a; var b = a;
  ```



- symbol

  ```typescript
  let sym = Symbol("key")
  console.log(sym)
  // error TS2585: 'Symbol' only refers to a type, but is being used as a value here. Do // you need to change your target library? Try changing 
  // the `lib` compiler option to es2015 or later.
  ```
  
  
  
  

### void

一般用来声明没有返回值的函数

声明一个变量为```void``` 没多大意义，因为一旦声明只能赋值为 ```null``` 和 ```undefinded```



### any

- 声明为 ```any``` 类型的变量，能被 赋值/修改 成任意类型的值

- ```any``` 类型的变量，可以访问任何属性，可以调用任何方法；那么，即操作返回的任何结果也是任意值

  ```typescript
  let v1 : any;
  console.log(v1.age)
  v1.getNum()
  let v2 : number;
  console.log(v2.age) // Property 'name' does not exist on type 'number'
  ```

- 变量声明时，若未指定类型，则默认被推论成 ```any``` 类型

  ```typescript
  // 以上指的是，声明同时未赋值的情况:
  let num
  num = 'a string'
  num = 11
  // 如果声明时赋值了，就会报错:
  let num = 11 // 这里根据类型推论规则，num被推论成number类型了
  num = 'a string'
  ```



### never

- 表示永不存在的值的类型
- 是所有类型的子类型，never类型的值可以赋值给任何类型的变量
- 除了never类型值，其他类型都不能赋值给never类型变量

- 返回never的函数必须有无法到达的终点：一般用于抛出异常 / 无限循环 情况下



### 数组

定义数组的方式：

- ```typescript
  // 数据类型[]
  let arr : number[] = []
  ```

- ```typescript
  // 泛型
  // Array[数据类型]
  let arr : Array<number> = []
  ```

- ```typescript
  let arr = new Array<number>(3); //undefinedx3 只是初始大小，后续可扩展
  ```



### 元组

新版本的TypeScript中，元组是有长度限制的，不能再进行跨界访问

```typescript
let v : [string,number]
v = ['a string', 11]
```



### 枚举 

[TypeScript enums: How do they work? What can they be used for?](https://2ality.com/2020/01/typescript-enums.html)

按枚举成员类型分类：

- 数字枚举

  ```typescript
  // 默认从0开始
  enum demo {
      a,
      b,
      c,
  }
  
  // 可以指定值
  enum demo1 {
      a = 11,
      b = demo.a,
      c = 33,
      d,
  }
  assert.equal(demo.a, 11)
  
  // 这样也可以
  enum demo {
      'a',
      'b',
      'c',
  }
  ```

- 字符串枚举

  ```typescript
  enum demo {
      a = 'hello',
      b = 'nihao',
      c = 'world',
  }
  ```

  

- 异构枚举

  ```typescript
  enum demo {
      a,
      b = 'nihao',
      c = 10,
      d,
  }
  // 使用：let v : demo = demo.a
  ```



按不同声明方式：

[typescript 枚举](https://www.jianshu.com/p/3a040670aa65)

[TypeScript enums explained](https://medium.com/@katbusch/typescript-enums-explained-e5f9a101afc9)

- 没有其他关键字
- const
- declare
- const declare





## 对象的类型——接口





# 联合类型

```typescript
let v : number | string
v = 1
v = 'a string'
```

```typescript
function getLength(something: string | number): number {
    return something.length; //只能访问共有的属性与方法
}
```


# 数组的类型



# 函数的类型