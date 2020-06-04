# props

组件实例的作用域是独立的，所以不应该在子组件里直接引用父组件的数据，通过props属性获得父组件的数据



## props的形式



### 字符串数组形式

```vue
// 子组件aChild: => 组件名采用驼峰形式，使用时采用中划线形式
<div>
    {{myTitle}}:{{myMessage}} // 在模板中插入，一律采用小驼峰形式
</div>

props:['my-message','myTitle'] // 一般采用中划线形式，也可以用小驼峰

// 父组件:
<a-child my-message='how are you' my-title='hello'></a-child> // 在父组件中赋值采用中划线
```



### 对象形式

```javascript
props:{
	myName:String,
	myAge:Number
}
```



#### 类型检测

**发生在组件实例创建之前**

- 基础类型
  
  ```javascript
  props:{
  	prop1: String
  }
  ```
  
  - null、undefined：支持任何类型
  - String
- Number
  - Boolean
  - Array
  - Object
  - Date
  - Function
  - Symbol
  
  
  
- 自定义类型

  ```javascript
  Person(name, age){
      this.name = name
      this.age = age
  }
Props:{
      prop1: Person
  }
  ```
  
  
  
- 多个可能的类型

  ```javascript
  props:{
  	prop1: [String, Number]
  }
  ```



- 带有默认值

  ```javascript
  props: {
  	prop1: {
  		type: String,
  		default: 'hello'
  	}
  }
  // 默认对象
  // 对象或数组默认值必须从一个工厂函数获取
  props: {
  	prop1: {
  		type: Object,
  		default: function() {
  			return { message:'hello' }
  		}
  	}
  }
  ```

  

- 有必填的值

  ```javascript
  props: {
  	prop1: {
  		type: String,
  		required: true
  	}
  }
  ```



- 自定义验证函数

  **传入的值必须使得 validator 的值为true，才通过验证**

  ```javascript
  props: {
  	prop1: {
  		validator: function (value){
  			// value必须是这三个值中的一个
  			return ['success', 'warning', 'danger'].indexOf(value) !== -1
  			// 又如：return value.length > 5
  		}
  	}
  }
  ```

  

## 静态/动态prop



### 传递静态prop

```vue
<template>
	<div></div>
	<a-child title='hello'></a-child>
</template>
```



### 传递动态prop

通过 ```v-bind``` 为 prop 动态赋值

```vue
<template>
	<div></div>
	// 即使赋的值是静态的，引号里面也不被解析成字符串而是js表达式了
	<a-child v-bind:title='infor.title'></a-child>
	<a-child :hasMsg='false' :person='{age:1,sex:male}'></a-child>
</template>
```

几种比较特殊的情况：

```vue
<template>
	<a-child v-bind='infor'></a-child> // 直接整个对象一起绑定,相当于: v-bind:title='' v-bind:time='' 
	<a-child hasMsg></a-child> // 没有赋值，即代表true
</template>
data(){
	return {
		infor: {
			title: 'hello',
			time: '2019'
		}
	}
}
```



## attribute

[vue中$attrs和$listeners以及inheritAttrs的用法](https://www.cnblogs.com/nayek/p/12052796.html)https://www.cnblogs.com/nayek/p/12052796.html)

### 带有prop的attribute / 非prop的attribute



父组件中没有在子组件的props中声明过的attribute，子组件可以通过 ```$attrs``` 获得



### 合并/代替attribute

class、style



### 禁用attribute

[关于vue.js里禁用特性继承的理解](https://blog.csdn.net/s_web_q/article/details/80239707)

```vue
<template>
	<label>
    	<input/>
    </label>
</template>
```

