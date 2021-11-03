# 浏览器端

1. 不同元素的css动画如何按顺序发生

   > 不同animation设置动画延迟，即等待几秒过后再开始此动画，时延短的动画先执行



2. transform

   > [transform属性详解](https://www.cnblogs.com/xiaohuochai/p/5351477.html)



3. 父元素div使用了min-height，但是当子元素超过父元素后div高度不随子元素变化

   > 1. 如果子元素脱离文档流，让子div的内容不脱离文档流，父div的高度就会跟随子div了
   > 2. 如果子div是浮动的，那父div加个overflow：hidden，浮动元素就占位了

   

4. 如何将html字符串通过art-template渲染成html原码   [参考art-template一些语法规则](<https://www.jianshu.com/p/b5dffff259be>)

   > **因为保护措施artTemplate会转义HTML代码为字符串输出，不需要转换时只需要前面加个@(旧版加#)**
   >
   > ```html
   > <script type="text/template" id="model">
   >  {{each article}}
   >  <p>{{$value.title}}</p>
   >  <p>{{$value.tag}}</p>
   >  <p>{{@($value.content)}}</p>  // 添加@表示输出html原码
   >  <p>{{$value.time}}</p>
   >  {{/each}}
   > </script>
   > ```
   > **ejs转换html字符串为html原码**
   > <%-xxx%>

   

5. 分页框，第一次点击无效，后续才生效

   > **该回调函数就是当点击分页按钮时触发的，参数是当前点击的按钮数字**。
   >
   > 并不需要再写点击事件
   >
   > ```javascript
   > /*原来写法*/
   > callback: function () { 
   >  $(".ui-pagination-page-item").click(function () {
   >      tempPage = $(this).getAttribute("data-current");
   >      $.ajax({
   >          url:'/showArticleList',
   >          type:'GET',
   >          dataType:'JSON',
   >          data:{
   >              page:tempPage
   >          },
   >          success:function (res) {
   >              var context = {article: res.articleList};
   >              var html = template('model',context);
   >              $('#article-list').html(html);
   >          }
   >      })
   >  })
   > }
   > ```
   >
   > ```javascript
   > /*纠正后*/
   > callback: function (tempPage) {
   >     console.log(tempPage);
   >     $.ajax({
   >         url: '/showArticleList',
   >         type: 'GET',
   >         dataType: 'JSON',
   >         data: {
   >             page: tempPage
   >         },
   >         success: function (res) {
   >             var context = {article: res.articleList};
   >             var html = template('model', context);
   >             $('#article-list').html(html);
   >         }
   >     })
   > }
   > ```



6. 如何选择同时具备两个class属性值的元素，如：```class = item active``` 

   > 1. 属性选择：```$("[class='item active']")```   // 前后顺序不能换
   > 2. 直接选择：```$(".box_list.clearfix")```



7. art-template的值作为变量传入方法中
   > ```'{{}}'```
   >
   > ```javascript
   > {{each article item index}}
   >  <div class="article-item">
   >      <div class="article-head">
   >          <h4 style="display: inline-block">{{item.title}}</h4>
   >          <span>{{item.time}}</span>
   >      </div>
   >      <div class="article-body" >
   >          {{@(item.content)}}
   >      </div>
   >      <div class="article-foot" >
   >          {{each item.tag}}
   >          <span>{{$value}}</span>
   >          {{/each}}
   >          <button onclick="deleteArticle('{{item.id}}','{{index}}')">删除                     </button>
   >          <button>修改
   >          </button>
   >      </div>
   >  </div>
   > {{/each}}
   > ```



8. ```<button type='submit' onclick='updateIt'>确认修改</button>```点击按钮后报错

   > 修改为```type = 'button'```



9. 关于js脚本执行顺序问题

   > manage.js 与 html内置脚本



10. $(this)和this

    > 



11. 获取name=xx的元素

    > ```$("[name = 'xx']")```



12. 判断空对象，为什么```req.query === {}```一直是false

    > ```JSON.stringify(req.query) === "{}"```能正确判断



13. 点击事件的参数是当前元素

    > onclick= 'fun(this)'  this  $(this)



14. 子元素浮动导致父元素坍塌

    > 1. 父元素设置overflow:hidden;



15. svg标签中的g标签作用

    > g元素这样的将多个元素组织在一起的元素。由g元素编组在一起的可以设置相同的颜色，可以进行坐标变换
    >
    > <svg width="100%" height="100%" version="1.1"
    > xmlns="http://www.w3.org/2000/svg">
    > <g fill="dodgerblue">
    >     <rect x="10" y="10" width="40" height="40" ry="10" />
    >     <rect x="80" y="80" width="40" height="40" ry="10" />
    >     <rect x="150" y="150" width="40" height="40" ry="10" />
    > </g>
    > </svg>



16. 手机端媒体查询失效原因

    > 没有添加：
    >
    > ```html
    > <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    > ```



17. 关于行内style优先级问题

    > ```html
    > <div class='tool' style='display:none'></div>
    > @media (max-width:414px){
    > 	.tool{
    > 		display:block;
    > 	}
    > }
    > // 移动端时无效
    > <div class='tool'></div>
    > .tool{
    > 	display:none;
    > }
    > @media (max-width:414px){
    > 	.tool{
    > 		display:block;
    > 	}
    > }
    > ```



18. 关于console.log

    ```javascript
    console.log("结果是:"+res); // 结果是[Object]
    //==========================================
    console.log("结果是:");
    console.log(res);
    //==========================================
    console.log("结果",res); // 结果 {xxx}
    ```

    

19. 使用fullPage.js插件页面刷新后只能回到顶部的情况
  
> 浏览器默认刷新后回到刷新前的位置，而不是顶部

   ```javascript
   $(document).ready(function(){
   $('#fullPage').fullPage({
        resize:false,
        anchors:["first","second","third","forth"], /* 只要写了这个就可以回到原来位置 */
        afterLoad:function(anchorLink, index){ // 滚动到当前section时触发
            // 将当前section的index存入sessionStorage
        // sessionStorage.setItem('currentSection',index);
           // var currentSection = sessionStorage.getItem('currentSection');
           // $.fn.fullpage.moveTo(currentSection);
        }
    })
   })
   ```



20. 导航栏 与 section 的互动

    > d

    ```html
    <ul id="menu">
        <li class="active" data-menuanchor="first"><a href="#first">我的首页</a></li>
        <li data-menuanchor="second"><a href="#second">技术博客</a></li>
        <li data-menuanchor="third"><a href="#third">作品展示</a></li>
        <li data-menuanchor="forth"><a href="#forth">资源下载</a></li>
    </ul>
    ```

    ```javascript
    $(document).ready(function(){
    $('#fullPage').fullPage({
         resize:false,
         anchors:["first","second","third","forth"], /* 只要写了这个就可以回到原来位置 */
         menu:"#menu"
     })
    })
    ```



21. 为什么显示[object]，而没有具体的值 [参考资料]( https://segmentfault.com/a/1190000007368846 )

    [json与js对象对比]( https://blog.csdn.net/Yeoman92/article/details/54924930 )

    ```javascript
    typeof()
    ```

    

22. 取出存入sessionStorage中的数，成了[object]

    ```javascript
    var data = {id:2,name:"Zia"}
    console.log(data.toString()); // [object]
    sessionStorage.setItem("infor",data);
    console.log(sessionStorage);
    var getData = sessionStorage.getItem("infor");
    console.log(getData);
    ```




23. ```val()``` 与 ```attr('value')```

    >  .val() 能够取到 针对text，hidden可输入的文本框的value值 
    >
    >  .attr('value') 可以取到html元素中所设置的属性 value的值，不能获取动态的如input type="text" 的文本框手动输入的值 






# 服务器端

1. 连接数据库操作

   > 

   

2. 提交的对象属性中带有连接符 "editor-html-code"，如何引用

   > ```var param = req.body; param['editor-html-code']```
   >
   > **对象.['属性']**

   

3. 数据库想根据操作时间自动添加时间字段

   > 字段类型设置成```timestamp```；然后勾选"根据当前时间戳更新"；最后属性值设为```CURRENT_TIMESTAMP```

   

4. res.end()报错 ```TypeError [ERR_INVALID_ARG_TYPE]: The "chunk" argument must be one of type string or Buffer. Received type object```

   > 比较 ```res.send()```   ```res.end()```   ```res.json()```    [参考资料](<https://blog.fullstacktraining.com/res-json-vs-res-send-vs-res-end-in-express/>)
   >
   > 1. ```res.send()```:
   >
   > 响应类型有Buffer、String、Array、Object
   >
   > 会根据相应数据自动设置响应头的Content-Type(也可以自己手动设置来改变)
   >
   > |        | Buffer                     | String      | Array            | Object           |
   > | ------ | -------------------------- | ----------- | ---------------- | ---------------- |
   > | 响应头 | application / octet-stream | text / html | application/json | application/json |
   >
   > 能响应JSON数据
   >
   > 
   >
   > 2. ```res.json()```:
   >
   > 一般用来响应JSON数据，但也可以将非JSON数据进行转换
   >
   > 响应头都是```application/json```
   >
   > > 与 ```res.send()``` 响应JSON数据有什么区别？
   > >
   > > 
   >
   > 
   >
   > ```res.end()```:
   >
   > 没有数据需要响应给客户端时使用，让客户端结束等待。```res.status(404).end();```



5. 获取不到rows的值
   ```javascript
   totalPage = db.query(sqlCommand.getAtcCount,function(err,rows){return rows.count;});
   ```
 ```

> callback回调




 ```



6. ```contentType``` 与 ```dataType```

   > ```contentType``` : 
   >
   > 客户端告诉服务器，自己要发什么类型数据
   >
   > 默认(未指定时)为 `'application/x-www-form-urlencoded; charset=UTF-8'`
   >
   >  W3C XMLHttpRequest标准规定，charset只设置为utf-8
   >
   > ```dataType``` : 
   >
   > 客户端告诉服务器，自己想要什么类型的数据
   >
   > 未指定时，根据服务器响应的MINE类型推测