# CSS选择器



## 有哪些选择器



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





## CSS样式的权重

