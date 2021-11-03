# 对Vue的理解

**渐进式**：主张少，开发者可以按需采用，可以仅仅把它作为一个小小的库而不必改变整个项目的逻辑，也可以做全家桶开发。





# Vue实例

- Vue实例 暴露的属性与方法，引用时的格式```xx.$xxx```，以防与用户自定义的属性分开

  ```javascript
  var vm = new Vue({
    el: '#demo',
      data: {
          a:1
      }
  })
  vm.a // 1
  vm.$data // {a:1}
  ```




## 属性

### $data 

[参考资料](<https://blog.csdn.net/weixin_36210698/article/details/85000575>)

- Vue实例创建时，data中的属性被添加到Vue的响应式系统中

- 因为Vue实例也代理了data对象的所有的属性，所以```vm.$data.a === vm.a```

- 只有当实例被创建时就已经存在于 `data` 中的属性才是响应式的

  ```javascript
  var vm = new Vue({
      el: '#demo',
      data: {
          information: [{
              name: "Qiyao",
              age: 20
          }, {
              name: "Xiaoyan",
              age: 22
          }]
      },
      methods:{
          grow:function(){
              this.information.push({name:"abc",age:40}); // 添加成功，且视图响应
              this.a = 123; // 未被添加到this.$data中，自然未被视图响应
              // 检验：
              console.log(Object.getOwnPropertyNames(this.$data).length); // 2
              /*为什么显示data对象有两个属性*/
              /* for(var item of arr){
      			console.log(item); // information 和 __ob__
      			// __ob__: Observer这些数据是vue这个框架对数据设置的监控器，一般都是不可枚举的
  			}*/
              console.log(Object.keys(this.$data)); // ["information"]
          }
      }
  })
  ```

  

## 生命周期钩子

- 生命周期

  > Vue实例，开始创建 &rarr; 初始化数据 &rarr; 编译模板 &rarr; 挂载DOM 渲染 &rarr; 更新 渲染 &rarr; 卸载 的过程

- 生命周期钩子

  > 让开发者在生命周期的不同阶段，可以添加不同事件方法

| 生命周期钩子  | 作用阶段                                                     |
| ------------- | ------------------------------------------------------------ |
| beforeCreate  | 实例创建之后，属性绑定之前(data未有响应性,events未活动)      |
| created       | 属性绑定之后(data有响应性,events活动)                        |
| beforeMount   | template和渲染方法编译完成；但实例未挂载到DOM (虚拟DOM，无法获取到DOM) |
| mounted       | 组件挂载完成，能获取到DOM (this.$el)                         |
| beforeUpdate  | data变化，update cycle开始后(可以获取变化后的data)；但DOM 还未重新渲染 |
| updated       |                                                              |
| activated     |                                                              |
| deactivated   |                                                              |
| beforeDestroy |                                                              |
| destroyed     |                                                              |































1. Vue使用cdn版本

2. 什么时候需要编译器+运行时的完整版本

3. 数据绑定到 DOM 文本或特性，还可以绑定到 DOM 结构

4. Vue的过渡效果系统

5. str.split('').reverse().join('')

   split(''): 分割每个字符组成数组

   join(''): 将数组元素连接成字符串

6. 所有的 DOM 操作都由Vue来处理，编写的代码只需要关注逻辑层面即可

7. Vue组件系统，方便前端组件复用

   为了使用结构相同数据不同的组件，用到```prop```

8. 模块化系统，方便代码分层开发，保证每个功能模块的职能单一

9. v-bind:key=""

10. 使用v-for渲染元素时，使用元素自身的id属性去指定渲染元素的key值有利于单个元素的重新渲染，若采用其他如v-for提供的index, key等值，在改变渲染出来的DOM结构时，会触发所有元素的**重新渲染**，当数据过大时，可能会造成性能负担

11. 所有的Vue组件都是Vue实例

12. 只有当实例被创建时就已经存在于 `data` 中的属性才是**响应式**的。因为所有的属性加入到 Vue 的**响应式系统**中 （Object.freeze(dataValue)使数据变化不再响应）

    所以尽可能要用到的赋初值

13. ```javascript
    var data = { a: 1 }
    var vm = new Vue({
      el: '#demo',
      data: data
    })
    vm.a // 1
    /**
    * .$属性 与 用户自定义的属性分开
    */
    vm.$data // { a: 1 }
    vm.$el //document.getElementById('demo')
    ```

    

14. 实例生命周期钩子（实例被创建后初始化过程中执行的一些函数）

    ​    

    ```javascript
    
    ```

    

