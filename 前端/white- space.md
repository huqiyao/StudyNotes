# white- space

|        属性         | 源码空白字符 |      源码换行符      | \<br>换行 | 容器边界换行 |
| :-----------------: | :----------: | :------------------: | :-------: | :----------: |
|   normal (默认值)   |  合并成一个  | 不换行，做空白符处理 |   换行    |     换行     |
|       nowrap        |  合并成一个  | 不换行，做空白符处理 |   换行    |   不会换行   |
|         pre         |     保留     |         换行         |   换行    |   不会换行   |
|      pre-wrap       |     保留     |         换行         |   换行    |     换行     |
|      pre-line       |  合并成一个  |         换行         |   换行    |     换行     |
| inherit：继承父元素 |              |                      |           |              |



## 与text-overflow结合

- 单行文本溢出显示省略号

  ```html
  <xx class='text'>abcdefghijklmnopqrstuvwxyz</xx>
  ```

  ```css
  .text{
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
  }
  ```

- 多行文本溢出显示省略号（即，一个段落查看更多浏览整篇文章的效果）

  [StackOverflow](https://stackoverflow.com/questions/3922739/limit-text-length-to-n-lines-using-css)
  
  [参考资料](https://www.cnblogs.com/hellman/p/5755376.html)
  
  [私有前缀](https://blog.csdn.net/jjting/article/details/38295441)
  
  ```css
  span{
      overflow: hidden;
    text-overflow: ellipsis;
      display: -webkit-box; // 将对象作为弹性伸缩盒子模型显示
    -webkit-line-clamp: 3; // 作用于块元素，控制文本展示的行数
      -webkit-box-orient: vertical; // 设置伸缩盒对象的子元素的排列方式 
  }
  ```
  
  存在问题：老版本的IE不支持
  
  ```scss
  // 多行文本截断
  @mixin multiLineEllipsis($lineHeight: 1.2em, $lineCount: 1) {
    $left: 2px;
    $dotTop: -1.5em;
    $dotWidth: 2.5em;
  
    &:before {
      content: '';
      float: left;
      width: $left;
      height: $lineHeight * $lineCount;
    }
    // 设置容器高度和行高
    & {
      overflow: hidden;
      position: relative;
      line-height: $lineHeight;
      height: $lineHeight * $lineCount;
    }
    // 设置子元素
    & > *:first-child {
      float: right;
      width: 100%;
      margin-left: 0-$left;
    }
  
    &:after {
      content: '\02026';
      box-sizing: content-box;
  
      float: right;
      position: relative;
      top: $dotTop; // 溢出时，出现
      left: 100%;
      width: $dotWidth;
      margin-left: 0-$dotWidth;
      padding-right: $left;
  
      text-align: right;
  
      background-size: 100% 100%;
      /* 512x1 image, gradient for IE9. Transparent at 0% -> white at 50% -> white at 100%.*/
      background: linear-gradient(
        to right,
        rgba(255, 255, 255, 0),
      white 50%,
        white
      );
    }
  }
  ```
  
  ```css
  /* mixin for multiline */
  .block-with-text {
    overflow: hidden;
    position: relative;
    line-height: 1.2em;
    max-height: 6em;
    text-align: justify;
    margin-right: -1em;
    padding-right: 1em;
  }
  .block-with-text:before {
    content: '...';
    position: absolute;
    right: 0;
    bottom: 0;
  }
  .block-with-text:after {
    content: '';
    position: absolute;
    right: 0;
  width: 1em;
    height: 1em;
    margin-top: 0.2em;
    background: white;
  }
  ```
  
  

## -webkit- 前缀

浏览器私有前缀，是浏览器对于新CSS属性的一个提前支持。-webkit-是webkit内核的，-moz-是Firefox Gecko内核，moz代表的是Firefox的开发商Mozilla。
为什么要有私有前缀呢？因为制定HTML和CSS标准的组织W3C动作是很慢的。通常，有w3c组织成员提出一个新属性，比如说圆角border-radius，大家都觉得好，但是w3c不会为这个属性制定标准，而是要走很复杂的程序，经过很多审查。而浏览器商不愿意等那么久，他们觉得一个属性已经够成熟了，就会在浏览器中加入支持。