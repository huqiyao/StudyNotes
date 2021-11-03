1. bootstrap、Vue等不下载，直接使用cdn版本

   > CDN(content delivery network)，内容分发网络
   >
   > 访问离自己最近的服务器以获得js等文件内容



2. Vue完整版(运行时+编译器)、运行时版

   > 需要在客户端编译template时，需要编译器，采用完整版



3. 在node与浏览器控制台中执行结果不同

   ```javascript
   var obj = {
     foo: function () { console.log(this.bar) },
     bar: 1
   };
   
   var foo = obj.foo; 
   var bar = 2;
   obj.foo(); // 1
   foo(); // result in chrome: 2; result in node: undefined
   ```

   > ```var``` 定义的变量，在node中是局部变量，而在浏览器环境下是全局变量
   >
   > 使用```strict``` ```mode``` 或者 改成 ```bar = 2``` 就会有相同的结果



4. 关于JavaScript的 ```this``` 导致的问题

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <meta http-equiv="X-UA-Compatible" content="ie=edge">
       <title>Document</title>
       <script src="https://cdn.jsdelivr.net/npm/vue"></script>
   </head>
   
   <body>
       <div id="lifecycle">
           <h1>{{ title }}</h1> 
            <button @click="title='New Title'">Update Title</button>
          </div>
       <script src='practice.js'></script>
   </body>
   
   </html>
   ```

   ```javascript
   new Vue({
       el:'#lifecycle',
       data:{
           title:'hello Vue'
       },
       beforeCreate:function(){
           console.log("beforeCreate()",this.title);
       },
       created:function(){
           console.log('created()',this.title);
       },
       beforeMount:function(){
           console.log('beforeMount()',this.$el);
       },
       mounted:function(){
           // setTimeout(function(){
           //     console.log('mounted()',this.$el); // undefined
           // },3000);
           
           // setTimeout(() => { console.log('mounted()',this.$el); },3000); // √
           
           // console.log('mounted()',this.$el); // √
       }
   })
   ```

   > ```this``` 指向的对象是谁的问题
   >
   > ```this``` 指向 拥有该 function 的 object



5. 获得窗口高度

   > ```javascript
   > $(window).height()+'px'
   > ```

