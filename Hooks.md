# useEffect

[三种形式的区别](#空[]，无[]，[xx]的区别)

<a>对变量的监测原理</a>

<a>使用场景</a>









## 空[]，无[]，[xx]的区别







# useState

<a>使用setState的原因</a>



## 直接改变this.state与setState

直接修改this.state的值，虽然事实上改变了组件的内部状态，但只是野蛮地修改了state，却没有驱动组件进行重新渲染，不会反应this.state值的变化；

而this.setState()函数做了两件事：1⃣️改变this.state的值，2⃣️驱动组件经历更新过程，让this.state里新的值出现在界面上。





