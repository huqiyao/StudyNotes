# 正则表达式

## 概念介绍

正则表达式:heart:  ：一种匹配模式，匹配字符、位置。可以模糊匹配、精确匹配，最大的作用还是用来模糊匹配



## 匹配字符

### 纵向模糊匹配

- 范围表示法 [1-9a-f]：1-9之间的一个数字 或 a-f之间的一个字母
- 字符组表示法 [abc]：a、b、c中的任意一个字符
- 排除字符组 \[^abc]：除了a、b、c之外的任意一个字符

| 字符组 | 含义                                                         |
| ------ | ------------------------------------------------------------ |
| \d     | [0-9]，一位数字                                              |
| \D     | [^0-9]，除了数字之外的其他字符                               |
| \w     | [0-9a-zA-Z_]，表示常规的单词字符                             |
| \W     | [^0-9a-zA-Z_]，表示非单词字符                                |
| \s     | [\t\v\n\r\f]，表示空白符号：空格、水平制表符、垂直制表符、换行符、回车符、换页符 |
| \S     | [^ \t\v\n\r\f]，表示非空白符                                 |
| .      | [^\n\r\u2028\u2029]，表示 除换行符、回车符、行分割符、段分隔符 外的任何字符 |



### 横向模糊匹配

量词，表示前面的字符重复出现多少次

| 量词 |              含义              |
| :--: | :----------------------------: |
| {m,} |          至少出现m次           |
| {m}  |         {m,m}，出现m次         |
|  ?   |      {0,1}，出现或不出现       |
|  +   |       {1,}，出现至少一次       |
|  *   | {0,}，出现任意次（可能不出现） |



#### 关于贪婪匹配与惰性匹配







## 例子



1. ```The colors of the rainbow have many colours and the rainbow does not  have a single colour.```
    - 找出colors、colours、colour        ```colou?rs?```




2. ```These are some phone numbers 915-555-1234,643.123.1333,(212)867-5509```

    - 找出5个字母组成的单词                  ```\b\w{5}\b```

      ```\w{5}``` : **These** are some **phone** **numb**ers …    (&times;)

      ```\w{5}\s``` : **These** are some **phone** nu**mbers** … (&times;)

    - 匹配电话号码 (字符分类)                ```\(?\d{3}[-.)\d{3}[-.]\d{4}]```

      > “(" 前面为什么要加 "\" ?    答：在[ ]外面，==**特殊字符**==都是要加”\“的
      >
      > 其他的包括：==**( [ { \ ^ $ | ) ? * + .]}**== 都要



3. ```javascript
    //多行文本
    This is somthing 
    is about
    a blah
    words
    sequence of words
    Hello and
    GoodBye and 
    Go gogo!
    ```
    - 匹配每行开头的单词：        ```^\w+```
    - 匹配每行结尾的单词：        ```\w+$```
    - 匹配每个单词的首字母：    ```\w```
    - 匹配每一个单词：                ```\w+```



4. ```javascript
   gaoyaqi411@126.com  
   dyumc@google.net 
   sam@sjtu.edu
   ```

   - 匹配所有邮箱：                   ```[\w.]+@\w+\.(com|net|edu)```      

     > 为什么不只是\w而是[\w.]     答：有些用户名是可能含有"."的



5. ```jav
   [google](http://google.com)
   [itp](http://itp.nyu.edu)
   [Coding Rainbow](http://codingrainbow.com)
   
   shiffina, Daniel
   shifafl, Daniell
   shquer, Danny
   
   This is a a dog , I think think this is is really
   a a good good dog. Don't you you thinks so so ?
   ```

   - 匹配link标签并将其替换成html标签 ：     

     ```reg : \[(.*?)\]\((http.*?)\)```     &gg;&gg;&gg;&gg;&gg;&gg;&gg;  通过"**?**"来实现**最小匹配(非贪婪)** + "**()**"**分组捕获**

     ```replace : <a href="$2">$1</a>```

   - 将姓和名互换位子 ：

     ```reg  :  (\w+),\s(\w+)```

     ```replace  :  $2  $1```

   - 匹配重复的两个单词  ：

     ```(\w+)\s\1```    &backsim;&backsim;&backsim;&backsim;&backsim;&backsim;&backsim;&backsim;&backsim;&rightsquigarrow;  **"\1":第一个括号捕获的内容** ，在正则表达式内使用，**$1**在表达式外使用

     ```(\w+)\s\1```   :  Th**is is a a** dog , I think this **is is** really **a a** dog. Don't **you you** thinks so so ?   (&times;)





## 在JavaScript中的应用

- 在js中，正则一般用于字符串

- 正则表达式本身有个```test()```方法(**检测是否包含**) 和  ```exec()```方法;  JavaScript中字符串也有关于正则的方法：

  ```javascript
  var str1 = "12"
  var str2 = "ab123"
  var r = /\d{3}/
  r.test(str1)  // false
  r.test(str2)  // true
  ```

  


  ### ```str.match()```  

 **返回了第一个可以匹配的序列**

> **想显示后续所有匹配的内容，怎么办**？   **答**：```flag```

| flag |    含义    |
| :--: | :--------: |
|  g   |  匹配全局  |
|  i   | 忽略大小写 |
|  m   |  匹配多行  |

```javascript
    var str = "Here is a Phone Number 111-2313 and 133-2311"
    var r1 = /\d{3}[-.]\d{4}/
    var r2 = /\d{3}[-.]\d{4}/g
    str.match(r1) // ["111-2313"]
    str.match(r2) // ["111-2313","133-2311"]
    
    var r3 = /(\d{3})[-.](\d{4})/ 
    str.match(r3) // ["111-2313","111","2311"] 未使用g，分组匹配仅显示第一个匹配的所有分组匹配
    var r4 = /(\d{3})[-.]\d{4}/g 
    str.match(r4) // ["111-2313","133-2311"] 使用了g后，不会显示分组
```
​                                      &Downarrow;
> **想显示全局的分组，怎么办？**    **答：正则表达式的执行方法**  ```reg.exec()```



### ```reg.exec()```

```reg.exec()```  **每次调用，返回一个**匹配的结果，匹配结果和分组以**数组的形式返回**，**不断的调用即可返回下一个**结果，**直到返回 null**   ==只有在有```g```标识时才这样，否则始终只返回第一个匹配与其分组组成的数组==

```javascript
// 演示
var str = "Here is a Phone Number 111-2313 and 133-2311"
var r = /(\d{3})[-.](\d{4})/g
var r2 = /(\d{3})[-.](\d{4})/
var result = r.exec(str)
while(result != null){
    console.log(result) 
    //打印出，第一次循环：["111-2313","111","2313"] 第二次循环：["1332311","133","2311"]
    result = r.exec(str)
}
console.log(r2.exec(str)) // ["111-2313","111","2313"]
console.log(r2.exec(str)) // ["111-2313","111","2313"]
console.log(r1.exec(str)) // ["111-2313","111","2313"]
console.log(r1.exec(str)) // ["1332311","133","2311"]
```



### ```str.split()```

**字符串按正则表达式所给的分隔规则，分隔形成数组**

```javascript
// 演示
var str = "unicorns and rainbows And, Cupcakes!"
str.split(" ")      // ["unicorns", "and", "rainbows", "And,", "Cupcakes"]
str.split(/\s/)     // ["unicorns", "and", "rainbows", "And,", "Cupcakes"]
str.split(/[,\s]/)  // ["unicorns", "and", "rainbows", "And,", "", "Cupcakes"]
str.split(/[,\s]+/) // ["unicorns", "and", "rainbows", "And", "Cupcakes"]
```

> **打印  ```str.split(/[,\s!]/)```  后，为什么数组中出现""(空字符串)？**
>
> **答**：&oplus; **split()工作过程**：遇到目标字符时，截取此目标字符位置之前且上一个目标字符位置之后的内容，组成字符串存入数组。 &oplus;**此例中**，遇到空格时，截取此目标字符位置之前且上一个目标字符“,”之后的内容，但**没有内容，所以形成空字符串**。&oplus; **所以改成**：**连续的逗号和空格被视为一个整体**



### ```str.replace()```

```str.replace(reg,newContent 或 function)```  :  将字符串中的指定内容替换成新内容

- 不会影响原字符串，只会**返回**新字符串

- 不使用  ```g```  时，也只会匹配替代一个

> 将字符串中的a、e、i、o、u重复写



### ```str.search()```

返回一个匹配此正则表达式的子字符串的位置索引，没有则返回-1

```javascript
var str = "nihaoma wohenhao"
console.log(str.search(/\w{2}o/))  // 3
```

