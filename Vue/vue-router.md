# vue-router

Vue 的 路由管理器



## 使用示例

```vue
<!-- src/App.vue -->
<template>
	<div id='app'>
        <router-view/>
    </div>
</template>
<script>
	export default{
        name: 'App',
    }
</script>
```

```javascript
/* src/Router/index.js */
import Router from 'vue-router'

Vue.use(Router)
export default new Router({
    base: '',
    mode: 'history',
    routes: [{name: '', path: '/index', component: ()=>import('../pages/xx.vue')},
             {...},
             {...},],
})
```

```javascript
/* src/main.js */
import router from './Router'
import App from './App'

new Vue({
    router,
    render: h => h(App),
}).$mount('#app')
```

[参考](https://blog.csdn.net/luoyu6/article/details/80098145)

```vue
<template>
	<div>
        <router-link :to='/index'>首页</router-link>
        <router-link :to='/about'>关于我们</router-link>
        <router-view />
    </div>
</template>
```



## 动态路由匹配

**作用**：利用某种模式，匹配到对应的多种路由，然后将其映射到同一个组件中

**注意**：使用路由参数时，如从 ```/user/101``` 导航到 ```/user/102```，组件会复用，不经历销毁重建过程，那么组件生命周期钩子不会被调用。

**优先匹配原则**：先定义，优先匹配

### 模式举例

- *
- /user-*

​          ⬇

使用通配符时，匹配到的路由会自动生成一个属性```pathMatch```，是填充通配符的内容（/admin: /admin, /user-name: name）

- /user/:name
- query方式怎么写？
- 。。。
- 高级匹配模式：**path-to-regexp**



## 监听路由的变化

- watch

  ```vue
  watch() {
  	$router(to, from){ // newVal,oldVal
  		
  	}
  }
  ```

  `$route` 作为vue实例的一个响应式属性，和在data中写的属性本质上是一样的。所以可以通过watch监听其变化

  

- 组件内 beforeRouteUpdate 钩子 

  ```vue
  beforeRouteUpdate(to, from, next){
  	
  }
  ```

  [钩子使用位置的错误](https://segmentfault.com/q/1010000015554869)



## 嵌套路由



## 导航守卫

