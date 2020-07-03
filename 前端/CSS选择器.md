# CSS选择器



## 有哪些选择器

[参考资料](https://juejin.im/post/5eaf64276fb9a0435749c23a#heading-21)

| 选择器         | 符号                                                         | 备注                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **基本选择器** |                                                              |                                                              |
| 通配符选择器   |                                                              |                                                              |
| 标签选择器     |                                                              |                                                              |
| 类选择器       |                                                              |                                                              |
| ID选择器       |                                                              |                                                              |
| **属性选择器** | [attr]<br>[attr=value]<br>[attr~=value]：属性里有一个值是value<br>[attr*=value]：只要有一个属性值含value子串即可<br>[attr\|=value]：attr=value 或 value-xx<br>[attr^=value]：只要有一个属性值是以value子串开头即可<br>[attr$=value]：只要有一个属性值是以value子串结尾即可<br> |                                                              |
| **分组选择器** | A,B ：匹配符合A的或者B的所有选择器                           |                                                              |
| **关系选择器** |                                                              |                                                              |
| 后代选择器     | A B                                                          |                                                              |
| 子选择器       | A > B                                                        |                                                              |
| 相邻兄弟选择器 | A+B ：只能选一个                                             |                                                              |
| 一般兄弟选择器 | A~B：选出所有兄弟                                            |                                                              |
| **伪选择器**   |                                                              |                                                              |
| 伪类选择器     | :root—文档根元素<br>elem: nth-child(n)—选择elem的父元素的第n个是elem的子元素<br>elem: nth-of-type(n)—选择elem的父元素的第n个同类型的子元素<br>elem: nth-last-child(n)—选择elem的父元素的倒数第n个是elem的子元素<br>elem: first-child—选择elem的父元素的第1个是elem的子元素<br>elem: last-child—选择elem的父元素的最后1个是elem的子元素<br>elem: first-of-type—选择elem的父元素的第1个同类型的子元素<br>elem: last-of-type—选择elem的父元素的最后1个同类型的子元素<br>elem: only-child—选出其父元素只有一个子元素且是elem的子元素<br>elem: only-of-type—选出elem的父元素只有一个子元素是elem的elem子元素<br/>[elem]: empty—选择没有子元素的（文本也是子元素）elem<br>a:link<br>a:active<br>elem:hover<br>a:visited<br>表单元素:focus—选出获得焦点的元素<br>单选按钮/复选框:checked<br>表单元素:enabled/disabled—选出已启用/禁用的元素<br>:not(elem)—选出非elem的元素 | 按（未在文档树内的）状态信息来选择元素<br>:hover 必须位于 :link 和 :visited 之后（如果存在的话），这样样式才能生效 |
| 伪元素选择器   | elem::first-line—选择文本的第一行<br>elem::first-letter—选择文本的第一个字<br>elem::before<br>elem::after<br>input::placeholder—选出input的placeholder<br>elem::selection—选择elem的直接的被光标选中的文本 | 选择无法用语义标签表达的实体，如::after                      |





## CSS样式的位置

优先级：内嵌样式 > 内联样式 > 外联样式





## CSS选择器的权重

**权重：作为相同元素有多个样式声明时，谁被谁覆盖的依据**

| 等级 | 内容                 | 权重 |
| ---- | -------------------- | ---- |
| 1    | 内联样式             | 1000 |
| 2    | ID选择器             | 0100 |
| 3    | 类、伪类、属性选择器 | 0010 |
| 4    | 标签、伪元素选择器   | 0001 |
| 5    | 通配符、关系选择器   | 0000 |

- 声明了 ! import 的样式优先级最高 (**尽量不要用吧**)
- 权值相等，则后定义的优先
- 继承的样式没有权值，即总能被覆盖



> Q

- 分组选择器的权值怎么没有？

  > 就看 逗号 "," 两边的选择器了，其权值决定匹配到的元素的样式是否被覆盖

- 想提高优先级怎么办呢？

  > - 尽量避免使用 ! important
  > - 在选择器前面多写几个选择器呗，这样权值加起来就高啦

- 怎样覆盖 ! important?

  > - 再写一条，或者在新写的前面加一个选择器
  >
  >   ```css
  >   .name {
  >       color: red !important
  >   }
  >   /* 1. */
  >   .name {
  >       color: black !important
  >   }
  >   
  >   /* 2. */
  >   div .name {
  >       color: black !important
  >   }
  >   ```