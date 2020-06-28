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

| 属性                                    | 可选值                           | 默认值 |
| --------------------------------------- | -------------------------------- | ------ |
| order                                   | number（可<0，数值越小排列越前） | 0      |
| flex-grow<br>：该item能获得多少剩余空间 | ≠负数                            | 0      |
| flex-shrink<br>：该item缩小多少         |                                  |        |
| flex-basis                              |                                  |        |
| flex                                    |                                  |        |
| align-self                              |                                  |        |

