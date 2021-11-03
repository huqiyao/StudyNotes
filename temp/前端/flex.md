# flex布局



## 容器属性



| 属性                                                         | 可选值                                                       | 默认值                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------ |
| **flex-direction**                                           | row、column、row-reverse、column-reverse                     | row                                                    |
| **justify-content**                                          | space-around、space-between、center、flex-start、flex-end    | flex-start                                             |
| **align-items**                                              | flex-start、flex-end、center、baseline、sketch               | sketch：items未设置height(width)或为auto时拉伸填满容器 |
| flex-wrap                                                    | wrap、nowrap、wrap-reverse                                   | nowrap                                                 |
| flex-flow<br>(flex-direction \| flex-wrap)                   |                                                              | row nowrap                                             |
| align-content<br>：多根轴线的对齐方式。即有≥2行items情况下使用 | center、space-around、space-between、flex-start、flex-end、stretch | stretch                                                |

- ```align-items：baseline``` 在 ```flex-direction:column``` 下会生效吗？



## 项目属性

| 属性                                                         | 可选值                                            | 默认值                                  |
| ------------------------------------------------------------ | ------------------------------------------------- | --------------------------------------- |
| **order**                                                    | number（可<0，数值越小排列越前）                  | 0                                       |
| **flex-grow**<br>：该item能获得多少剩余空间，众多flex-grow共同决定扩大系数 | number (≠负数)                                    | 0                                       |
| **flex-shrink**<br>：该item缩小多少，众多flex-shrink共同决定缩小系数<br>只在超过容器范围(且nowrap)时生效 | number (≠负数)                                    | 1                                       |
| **flex-basis**<br/>：用来在分配剩余空间或缩小时，参与决定系数<br>优先级比item自身的height、width高 | auto、number、px、<br>％：相对于父元素            | auto（即item本身的height/width）        |
| **flex**<br/>：flex-grow [flex-shrink] [flex-basis]          | auto(1 1 auto)<br/>none(0 0 auto)<br/>...其他组合 | 0 1 auto                                |
| **align-self**<br>：控制某个item的align-items的              | flex-start、flex-end、center、baseline、sketch    | auto（继承父元素，没有父元素则stretch） |



### flex-grow 与 flex-shrink 的计算

- flex-grow

  假设： ①多出的空间：300；②flex-flow的值分别为1， 2， 3；③item的**flex-basis**分别为：100，50，100

  则 ： 1n✖100 ➕ 2n✖50 ➕ 3n✖100 = 300  ➡ 扩大系数：n=0.6

  item1：100✖(1+0.6)	item2：50✖(1+1.2) 	item3：100✖(1+1.8)

- flex-shrink

  假设：①缺少的空间：100，......其余同上
  
  则 ： 1n✖100 ➕ 2n✖50 ➕ 3n✖100 = 100 ➡ 缩小系数：n = 0.2
  
  item1：100✖(1-0.2)	item2：50✖(1-0.4) 	item3：100✖(1-0.6)



### 关于flex-basis

[参考资料](https://www.jianshu.com/p/17b1b445ecd4)

- ```flex-basis``` 优先级 ＞ ```width``` 优先级，即两者都存在时，采用 ```flex-basis``` 值。所以设置了 ```flex-basis``` 就不要设 ```width``` 了
- item 没有设置 ```flex-basis``` ，即为默认的```auto```，等于 ```width``` 的值
- 假如也没有 ```width```，那么 ```flex-basis``` 相当于 content 大小 
- ```max-width``` 、```min-width``` 会限制 ```flex-basis``` 的值



#### 与flex-wrap配合使用

[参考](https://blog.csdn.net/lmmxxoo/article/details/83094818)

子元素flex-basis之和大于容器宽度  + flex-wrap : wrap => 元素换行 => 换行的元素在新行内继续平分



### 实例分析

- 一个父元素下，要求：有两个子元素，分别占父元素的50%，且分别有20px、50px的padding。请计算下面三种情况

  >  box-sizing：content-box 时，参与计算的容器空间差值需要加工：
  >
  > finalValue = box-width - 子padding - 子border
  >
  > box-sizing：border-box 时，参与计算时的flex-basis值需要加工：
  >
  > finalValue = flex-basis - padding - border

  

  - 代码1

    ```html
    <head>
      <style>
        .box {
          display: flex;
          width: 400px;
        }
    
        .item-2-1 {
          flex: 1 1;
          padding: 50px;
          background-color: #32d6d6;
        }
    
        .item-2-2 {
          flex: 1 1;
          padding: 20px;
          background-color: #b85ad0;    
        }
      </style>
    </head>
    <body>
      <div class="box">
        <div class="item-1">1</div>
        <div class="item-2">2</div>
      </div>
    </body>
    ```

    

  - 代码2

    ```html
    <head>
      <style>
        .box {
          display: flex;
          width: 400px;
        }
    
        .item-1 {
          flex: 1 1 100%;
          padding: 50px;
          background-color: #32d6d6;
        }
    
        .item-2 {
          flex: 1 1 100%;
          padding: 20px;
          background-color: #b85ad0;    
        }
      </style>
    </head>
    <body>
      <div class="box">
        <div class="item-1">1</div>
        <div class="item-2">2</div>
      </div>
    </body>
    ```

    

  - 代码3

    ```html
    <head>
      <style>
        .box {
          display: flex;
          width: 400px;
        }
    
        .item-1 {
          flex: 1 1 100%;
          padding: 50px;
          background-color: #32d6d6;
          box-sizing: border-box;
        }
    
        .item-2 {
          flex: 1 1 100%;
          padding: 20px;
          background-color: #b85ad0;  
          box-sizing: border-box;
        }
      </style>
    </head>
    <body>
      <div class="box">
        <div class="item-1">1</div>
        <div class="item-2">2</div>
      </div>
    </body>
    ```

    