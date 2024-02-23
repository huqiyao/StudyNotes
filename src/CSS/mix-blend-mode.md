# 背景

![mix-blend-mode-1](/Users/qiyao/Documents/StudyNotes/src/CSS/assets/mix-blend-mode-1.png)

如上图，图片背景是白色的，放置在灰色容器中很突兀。有什么办法可以去掉白色，让图片与灰色容器容器融为一体呢？

可以用一个 css 属性： mix-blend-mode 



# mix-blend-mode



## 介绍

控制几个元素 ( 包括伪元素 ) 在重叠部分的混合效果。有这些混合效果：

![mix-blend-mode-3](/Users/qiyao/Documents/StudyNotes/src/CSS/assets/mix-blend-mode-3.png)



## 如何混合



![multiple-layers](/Users/qiyao/Documents/StudyNotes/src/CSS/assets/multiple-layers.png)



以像素点为单位，从[底层到顶层](https://css-tricks.com/taming-blend-modes-difference-and-exclusion/)，将对应位置的像素点进行两两比较，比较时根据 mix-blend-mode 的属性值不同，进行相应的混合计算。



## darken



![calculate-1](/Users/qiyao/Documents/StudyNotes/src/CSS/assets/calculate-1.png)

1. 如上图，虚线框内是重叠区域。我们的需求是将白色部分混合成灰色。我们采用darken模式（**选取较暗的颜色值作为新颜色，即通道颜色数值更小的**）进行颜色通道计算：

|      | #EDEDE9 RGB(237, 237, 233) | #000000 RGB(255, 255, 255) | 混合后结果 |
| ---- | -------------------------- | -------------------------- | ---------- |
| R    | 237                        | 255                        | 237        |
| G    | 237                        | 255                        | 237        |
| B    | 233                        | 255                        | 233        |

上面表格我们只列举了图片白色背景和容器的像素点混合过程，图片主体部分同理都会进行上述混合计算。



![calculate-2](/Users/qiyao/Documents/StudyNotes/src/CSS/assets/calculate-2.png)

2. 再来计算一下上图的例子，容器 #F6F6F4，图片背景部分 #F1F2F5

|      | #F6F6F4 RGB(246, 246, 244) | #F1F2F5 RGB(241, 242, 245) | 混合后结果 |
| ---- | -------------------------- | -------------------------- | ---------- |
| R    | 246                        | 241                        | 241        |
| G    | 246                        | 242                        | 242        |
| B    | 244                        | 245                        | 244        |

最终的结果是 RGB(241, 242, 244)，所以图片没法和容器背景融合。



## lighten

与 darken 一样的计算方法，只不过和 darken 相反，取通道颜色数值大的



## difference

取通道颜色之差

|      | #F6F6F4 RGB(246, 246, 244) | #F1F2F5 RGB(241, 242, 245) | 混合后结果      |
| ---- | -------------------------- | -------------------------- | --------------- |
| R    | 246                        | 241                        | \|246-241\| = 2 |
| G    | 246                        | 242                        | 242             |
| B    | 244                        | 245                        | 244             |

