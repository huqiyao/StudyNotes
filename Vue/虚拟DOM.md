# 虚拟DOM

[h函数](https://blog.csdn.net/qq_42778001/article/details/95959531)

组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。只有当它插入文档以后，才会变成真实的 DOM 。
有时需要从组件获取真实 DOM 的节点，这时就要用到 ref 属性