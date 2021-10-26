# Hooks



* [为什么要产生Hooks](#为什么要产生Hooks)
* [关于Hooks](#关于Hooks)
* [常用Hooks](#常用Hooks)
  * [useState](#useState)
* [引用](#引用)

<br/>

<br/>

## 为什么要产生Hooks

<br/>

- **函数组件更合适。** React 组件的本质就是将 model 渲染成 view ( *<u>UI=render(state, props)</u>* )，使用 class 创建组件不符合这样的思想，而且有些大材小用，因为class的一些特性完全没被利用：
  - 组件之间不是继承关系，未用到class类的继承特性
  - 组件不需要在外部调用那些实例方法
- **函数组件功能不足。**
  - 无法存在内部state（*<u>函数和对象不同，并没有⼀个实例的对象能够在多次执⾏之间保存状态，那势必需要⼀个函数 之外的空间来保存这个状态</u>*）
  - 没有生命周期机制



:question: 组合和继承

<div align='center' ><img src='../../../../assets/images/组合继承疑问.png' height='300px' width='500px'/></div>



## 关于Hooks

- :wrench:  <u>作用</u>：将某个目标结果钩到某个可能会变化的数据源或事件源上，当被钩到的数据或事件发生变化时，产生这个目标结果的代码会重新执行，产生更新后的新结果。**所有的 Hooks 的最终结果都是导致 UI 的变化。**

  <u>Hooks 提供了监听某个数据变化的能⼒。这个变化可能会触发组件的刷新，也可能是去创建⼀个副作⽤，⼜或者是刷新⼀个缓存。那么定义要监听哪些数据变化的机制，其实就是指定 Hooks 的依赖项。</u>

<div align='center' ><img src='../../../../assets/images/Hooks钩子.png' height='200px' width='500px'/></div>



- :boom:  <u>caution</u>：
  - Hooks必须被执行到（所以不能写在if、for等语句中，不能放在return后）
  - Hooks按顺序被执行
  - 只能出现在函数组件的顶级作用域 或者 其他自定义Hooks中



- :+1: <u>优点</u>：

  - 逻辑复用：class 组件只能通过高阶组件，代码不直观难理解而且会在外层产生额外组件节点

    ```tsx
    // 高阶组件复用方式
    const withWindowSize = (component)=>{
      class WrappedComponent extends React.PureComponent{
        constructor(props){
          super(props)
          this.state = {
            size: this.getSize()
          }
        }
        componentDidMount(){
          window.addEventListener('resize', this.handler)
        }
        componentWillUnMount(){
          window.removeEventListener('resize', this.handleRedize)
        }
        getSize(){
          return window.innerHeight > 1000? 'large': 'small'
        }
        handler(){
          const currentSize = this.getSize()
          this.setState({
            size: currentSize
          })
        }
        render(){
          return <Component size={this.state.size}/>
        }
      }
      return WrappedComponent;
    }
    // 使用
    class MyComponent extends React.Component({ size }){ 
      render() { 
        if (size === "small") return <SmallComponent />; 
        else return <LargeComponent />; 
      } 
    }
    withWindowSize(MyComponent)
    ```

    

    ```tsx
    // hooks方式
    const getSize = ()=>{
      return window.innerWidth > 1000? 'large': 'small'
    }
    const useWindowSize = ()=>{
      const [size, setSize] = useState(getSize())
      useEffect(()=>{
        const handler = setSize(getSize())
        window.addEventListener('resize', handler)
        return ()=>{
          window.addEventListener('resize', handler)
        }
      },[])
      return size
    }
    // 使用
    const MyComponent = ()=>{
    	const size = useWindowSize()
      return {size === 'small'? <SmallComponent />: <LargeComponent /> }
    }
    ```

    <br/>

  - 有助于关注分离：Hooks 能够让针对同⼀个业务逻辑的代码尽可能聚合在⼀块⼉。 Class 组件中，不得不把同⼀个业务逻辑的代码分散在不同⽣命周期的⽅法中。

<br/>

<br/>

## 常用Hooks



### useState

- :boom:  <u>caution</u>：
  - state不要保存可以通过计算得到的值。如从props传进来的值，从url中读出来的值，从cookie、storage中读出来的值……，需要的时候再取即可
  - 

<br/>

### useEffect

```tsx
useEffect(callback, dependencies)
```



- :wrench:  <u>作用</u>：执行副作用。在函数组件的当次执⾏过程中，useEffffect 中代码的执⾏是不影响渲染出来的 UI 的。



- :boom:  <u>caution</u>：

  - 不填 dependencies，则在每次 render 后都执行；

    dependencies 是空数组，则只在组件首次渲染时才执行，即相当于 **componentDidMount** ；

    dependencies 是包含指定值的数组，则只在指定值变化后才执行，即相当于 **componentDidUpdate**；

  - 在 useEffect 中 return 一个匿名函数，则相当于 **componentWillUnMount**

  - 对依赖项的监听，是一种**浅比较**(===)

  - 依赖项目需要在callback中用到，否则无意义



- :question:  <u>问题</u>：
  - 在 useEffffect 中如果使⽤了某些变量，却没有在依赖项中指定，会发⽣什么呢？ 
  - 对于这节课中显⽰的 Blog ⽂章的例⼦，我们在 useEffffect 中使⽤了 setBlogContent 这样⼀个函数，本质上它也是⼀个局部变量，那么这个函数需要被作为依赖项吗？为什么？ 

<br/>
<br/>

## 引用

- [1] [ReactHooks核心原理与实战-极客时间-王沛](https://pan.baidu.com/mbox/homepage#share/type=session)
