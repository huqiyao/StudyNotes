# Hooks



* [为什么要产生Hooks](#为什么要产生Hooks)
* [关于Hooks](#关于Hooks)
* [常用Hooks](#常用Hooks)
  * [useState](#useState)
  * [useEffect](#useEffect)
  * [useCallback](#useCallback)
  * [useMemo](#useMemo)
  * [useRef](#useRef)
  * useContext
  * useReducer
* [自定义Hooks](#自定义Hooks)
* [useId](#useId)
* [构造一次性执行代码](#构造一次性执行代码)
* [保证状态一致性](#保证状态一致性)
  * [state最小化](#state最小化)
  * [避免中间状态,确保唯一数据源](#避免中间状态,确保唯一数据源)
* [向服务器端发送请求](#向服务器端发送请求)
  * [封装自定义Hooks](#封装自定义Hooks)
  * [多个API调用如何处理并发串行请求](#多个API调用如何处理并发串行请求)
* [函数组件设计模式:复杂条件渲染场景](#函数组件设计模式：复杂条件渲染场景)
  * [容器模式:按条件执行Hooks](#容器模式:按条件执行Hooks)
  * [使用```render props```模式重用UI逻辑](#使用```render props```模式重用UI逻辑)
* [事件处理:创建自定义事件](#事件处理:创建自定义事件)
  * [原生事件](#原生事件)
  * [自定义事件](#自定义事件)


* [class组件和函数组件共存问题](#class组件和函数组件共存问题)
* [引用](#引用)



<br/><br/>

## 为什么要产生Hooks

<br/>

在函数组件中你要思考的方式永远是：当某个状态发生变化时，我要做什么，而不再是在 Class 组件中的某个生命周期方法中我要做什么

- **函数组件更合适。** React 组件的本质就是将 model 渲染成 view ( *<u>UI=render(state, props)</u>* )，使用 class 创建组件不符合这样的思想，而且有些大材小用，因为class的一些特性完全没被利用：
  - 组件之间不是继承关系，未用到class类的继承特性
  - 组件不需要在外部调用那些实例方法
- **函数组件功能不足。**
  - 无法存在内部state（*<u>函数和对象不同，并没有⼀个实例的对象能够在多次执⾏之间保存状态，那势必需要⼀个函数之外的空间来保存这个状态</u>*）
  - 没有生命周期机制



:question:&nbsp;组合和继承

<div align='center' ><img src='../../../../assets/images/组合继承疑问.png' height='300px' width='500px'/></div>

<br/><br/>

## 关于Hooks

<br/>

- :wrench: &nbsp;<u>作用</u>：将某个目标结果钩到某个可能会变化的数据源或事件源上，当被钩到的数据或事件发生变化时，产生这个目标结果的代码会重新执行，产生更新后的新结果。**所有的 Hooks 的最终结果都是导致 UI 的变化。**

  <u>Hooks 提供了监听某个数据变化的能⼒。这个变化可能会触发组件的刷新，也可能是去创建⼀个副作⽤，⼜或者是刷新⼀个缓存。那么定义要监听哪些数据变化的机制，其实就是指定 Hooks 的依赖项。</u>

<div align='center' ><img src='../../../../assets/images/Hooks钩子.png' height='200px' width='500px'/></div>



- :boom:&nbsp; <u>caution</u>：
  - Hooks必须被执行到（所以不能写在if、for等语句中，不能放在return后）
  - Hooks按顺序被执行
  - 只能出现在函数组件的顶级作用域 或者 其他自定义Hooks中



- :+1:&nbsp;<u>优点</u>：

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

    <br/>

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

<br/><br/>

## 闭包陷阱

[闭包笔记](../../../ECMAScript/闭包.md)

[掘金讲解](https://juejin.cn/post/6844904006079217672)

<br/>

jjjjj





<br/><br/>

## 常用Hooks

<br/>

### useState

<br/>

- :boom:&nbsp;<u>caution</u>：
  - state 不要保存可以通过计算得到的值。如从 props 传进来的需要加工的值，从 url 中读出来的值，从cookie、storage 中读出来的值……，需要的时候再取即可。
  
    因为否则就需要维护源 state 和目标 state 的一致性，会带来各种复杂度。
  
- :question:&nbsp;<u>问题</u>：

  - 函数组件重新执行，useState怎么操作？

    > 破案了！“useState 其实也是能够在组件的多次渲染之间共享数据的，那么在 useRef 的计时器例子中，我们能否用 state 去保存 window.setInterval() 返回的 timer 呢？”

<br/>

### useEffect

<br/>

```tsx
useEffect(fn, dependencies)
```

<br/>

- :wrench:&nbsp;<u>作用</u>：**每次 render 完后根据依赖项判断是否执行副作用**。(为什么叫副作用？在函数组件的当次执⾏过程中，useEffffect 中代码的执⾏是不影响渲染出来的 UI 的)



- :boom:&nbsp;<u>caution</u>：

  - 不填 dependencies，则在每次 render 后都执行；

    dependencies 是空数组，则只在组件首次渲染时才执行，即相当于 **componentDidMount** ；

    dependencies 是包含指定值的数组，则只在指定值变化后才执行，即相当于 **componentDidUpdate**；**但是第一次mount，即componentDidMount也会执行**。

  - 在 useEffect 中返回一个清除函数，在下一次依赖项发生变化时（即下一次副作用callback执行前，目的是清理上一次副作用）及组件卸载前（componentWillUnmount）执行。场景：setTimeout和clearTimeout、监听和取消监听等。

  - 对依赖项的监听，是一种**浅比较**(===)。

    ```tsx
    const todos = [{ text: 'Learn hooks.'}]; 
    useEffect(() => { console.log('Todos changed.'); }, [todos]); // todos在每次render时都重新赋值了，所以todos变化了即使内容没变化
    // 用useMemo即可(如果是函数，则用useCallback)
    const todos = useMemo(()=>[{ text: 'Learn hooks.'}], [])
    ```
  
    
  
  - 在callback中用到的属性需要在写在依赖项中，否则无意义。而且由于闭包的原因可能无法得到预期结果。<span style='color:red'>如果依赖项未被用到，但是作为flag来控制副作用执行呢</span>



- :question:&nbsp;<u>问题</u>：
  - 在 useEffffect 中如果使⽤了某些变量，却没有在依赖项中指定，会发⽣什么呢？ 
  
    > 1⃣️&nbsp;如果useEffect 没有依赖项参数情况下，则在每次render后都会执行副作用
    >
    > 2⃣️&nbsp;如果useEffect 有依赖项情况下，则即使该变量更新了也不会执行副作用
  
  - 在 useEffffect 中使⽤了 setXX 这样⼀个函数，本质上它也是⼀个局部变量，那么这个函数需要被作为依赖项吗？为什么？ 
  
    > useState 保证了 setXX 每次render时不发生变化。所以不需要作为依赖项
  
  - 如何实现componentWillUnmount的效果呢？
  
    > 依赖项为空数组，然后再写清除函数
    
  - ```useEffect(()=>{},[])```，执行副作用是在render完成后执行的，如果某些方法想在执行时只执行一次呢？
  
    > 如下，利用useRef[构造一次性执行代码](#构造一次性执行代码)
    
  - 如何让副作用只在依赖变化后执行
  
    > ```tsx
    > const isMounted = useRef(false)
    > useEffect(()=>{
    >   if(!isMounted.current){
    >     isMounted.curent = true
    >     return
    >   }
    >   doSomething() // 执行副作用
    > },[dep])
    > ```
    
    

<br/>

### useCallback

<br/>

```javascript
useCallback(fn, dependencies)
```



<br/>

- :cake:&nbsp;<u>背景</u>：函数组件每一次render总是重新执行整个函数。所以一个函数定义总是被重复执行，生成一个新函数，这种情况下如果函数作为子组件的prop，会导致子组件一直更新*<u>【不做任何处理情况下，父组件重新render(prop、state变化)总是造成子组件更新，在这里指的是子组件使用了React.memo的情况】</u>*。

  ```tsx
  const AComponent = ()=>{
    const [age, setAge] = useState(0)
    const handleIncrement = ()=> setAge(age+1) // 每次都生成新函数，而且作为prop传入子组件子组件会重新渲染
    // 
    return <button onClick={handleIncrement}/>
  }
  ```

  

- :chestnut:&nbsp;<u>例子</u>：

  ```tsx
  JumpItem组件
  ```

  

- :wrench:&nbsp;<u>作用</u>：只在依赖项更新时，才重新定义函数

- :boom:&nbsp;<u>caution</u>：

  - 如果依赖参数是空数组[]，那么只在组件mounting时执行一次

  - useCallback可以用useMemo实现的

    ```tsx
    const func = useCallback(()=>setCount(count+1),[count])
    // 等同于
    const func = useMemo(()=>{
      return ()=>setCount(count+1)
    },[count])

- :question:&nbsp;<u>问题</u>：

  - 对于```const handle = useCallback(()=>setCount(count+1),[])```，调用 handle时 coun t一直是 useState 时创建的初始值。count 是组件函数里的值，它是动态变化的，为什么 func 里的 count一直不变呢？
    > 破案啦。闭包 + 函数多次执行
    > ```tsx
    > const App = ()=>{
    >   const [count, setCount] = useState(0)
    >   const handle = useCallback(()=>{
    >     console.log(count)
    >   },[])
    >   return 
    >   <div>
    >   	<button onClick={()=>setCount(count+1)}></button>
    >     <button onClick={handle}></button>
    >   </div>
    > }
    > App()
    > // handle的闭包[{count:1}],
    > // 点击button1，促使render
    > App()
    > ```
    >
    
  - 那定义一个函数是否都需要使用useCallback包裹呢？
  
    > 一般那种作为prop传入子组件的才有必要用useCallback



<br/>

### useMemo

<br/>

```javascript
useMemo(fn, dependencies)
```

<br/>

- :cake:&nbsp;<u>场景</u>：一个比较复杂的变量，每次render都需要重新计算来赋值，作为子组件的prop还会造成子组件更新

- :wrench:&nbsp;<u>作用</u>：只有依赖项更新时，才需要重新生成返回值

- :chestnut:&nbsp;<u>例子</u>：

  ```tsx
  ma中的columns
  ```

  

<br/>

### useRef
<br/>

- :cake:&nbsp;<u>场景</u>：函数组件每次render都从头执行一遍，定义的变量也被初始化赋值了，没法在多次渲染间共享
- :wrench:&nbsp;<u>作用</u>：
  - 创建一个容器（相当于class组件的this吗？），保存跨渲染数据
  
  - 解决闭包陷阱
  
    ```tsx
    // 自定义 usePrevious hook
    ```
  
    
  
  - 保存一个DOM节点的引用，便于操作改节点
  
- :chestnut:&nbsp;<u>例子</u>：

  ```tsx
  // 保存跨渲染数据
  import React, { useState, useCallback, useRef } from "react";
  
  export default function Timer() {
    const [time, setTime] = useState(0);
    const timer = useRef(null);
  
    const handleStart = useCallback(() => {
      timer.current = setInterval(() => {
        setTime((time) => time + 1);
      }, 100);
    }, []);
  
    const handlePause = useCallback(() => {
      clearInterval(timer.current);
      timer.current = null;
    }, []);
  
    return (
      <div>
        {time / 10} seconds.
        <br />
        <button onClick={handleStart}>Start</button>
        <button onClick={handlePause}>Pause</button>
      </div>
    );
  }
  ```

  <br/>

  ```tsx
  // 保存DOM引用
  const wrapperRef = useRef(null)
  ...
  <div ref={wrapperRef}>
  	<Select getContainer={()=>wrapperRef.current}/>
  </div>
  ```




- :question:&nbsp;<u>问题</u>：

  - 和 createRef 比，其何如？

    > 每次render，createRef 都会返回一个新的引用，而 useRef 每次都会返回相同的引用。
    >
    > [掘金demo](https://juejin.cn/post/6844904062681350157)
    >
    > ```tsx
    > const Demo = ()=>{
    >   const [count, setCount] = useState(0)
    >   const aUseRef = useState(null)
    >   const aCreateRef = useState(null)
    >   if(aUseRef.current === undefined){
    >     aUseRef.current = count
    >   }
    >   if(aCreateRef.current === undefined){
    >     aCreateRef.current = count
    >   }
    >   return <div>
    >   	<button onClick={()=>setCount(count+1)}></button>
    >     <span>{aUseRef.current}</span>  {/*一直为0*/}
    >     <span>{aCreateRef.current}</span> {/*增加ing*/}
    >   </div>
    > }
    > ```

<br/>

### useContext

<br/>

- :wrench:&nbsp;<u>作用</u>：获得组件树的值

<br/>

### useReducer



<br/><br/>

## 自定义Hooks

<br/>

- :triangular_flag_on_post:&nbsp;<u>特征</u>：use开头、内部使用了其他hooks

- :chestnut:&nbsp;<u>例子</u>：

  - **抽取业务逻辑**：计数器

    ```tsx
    const useCounter = ()=>{
      const [count, setCount] = useState(0);
      const increment = useCallback(() => setCount(count + 1), [count]);
      const decrement = useCallback(() => setCount(count - 1), [count]);
      const reset = useCallback(() => setCount(0), []);
      return { count, increment, decrement, reset };
    }

  - **封装通用逻辑**：异步获取数据

    ```tsx
    const useAsync = (asyncFunc)=>{
      const [error, setError] = useState(null)
      const [data, setData] = useState(null)
      const [loading, setLoading] = useState(false)
      const execute = useCallback(()=>{
        setLoading(true)
        // setData、setError
        return asyncFunc().then((data)=>{ // 因为没有返回需要处理的数据，其实不return也可以
          setData(data)
          setLoading(false)
        }).catch((err)=>{
          setError(err)
          setLoading(false)
        })
      },[asyncFunc])
    }
    // 使用
    const {error, data, loading, execute} = useAsync(useCallback(async ()=>{
      const res = await fetch('/project/messages/getAll')
      const json = await res.json()
      return json.data()
    },[]))

  - **监听浏览器状态**：获得滚动条位置

    ```tsx
    const getPosition = ()=>{
      return {
        x: document.body.scrollLeft,
        y: document.body.scrollTop
      }
    }
    const useScroll = ()=>{
      const [position, setPosition] = useState(getPosition())
      useEffect(()=>{
        const handler = ()=> setPosition(getPosition(document)) // 为什么传入document
        document.addEventListener("scroll", handler)
        return ()=>{
          document.removeEventListener("scroll", handler)
        }
      },[])
      return position
    }
    // 回到顶部组件，使用
    const { y } = useScroll() 
    const toTop = useCallback(()=>{
      document.body.scrollTop = 0;
    },[])
    if(y > 300){
      return <button onClick={toTop}>回到顶部</button>
    }
    return null;

  - **拆分复杂组件**。Hooks就像普通函数一样，可以使用自定义hooks来隔离业务代码，然后在函数组件里直接使用hooks以避免组件太长。

    ```tsx
    // 获得文章
    const useArticle = ()=>{
      const {error, data, loading, execute} = useAsync(useCallback(async ()=>{
      	const res = await fetch('/project/messages/getAll')
        // res.json是个promise，所以需要await
      	const json = await res.json() 
      	return json.data()
    	},[]))
      useEffect(()=>{
        execute()
      },[execute])
      return {
        article: data, 
        articlesLoading: loading,    
        articlesError: error}
    }
    // 获得评论同理
    const useComment = ()=>{}
    ```
    
    



# useId





## 构造一次性执行代码



```tsx
const useOnce = (callback)=>{
  const called = useRef(false) // called:{ current: false}
  if(called.current){
    return
  }
  callback()
  called.current = true
}

const Demo = ()=>{
  useOnce(()=>{ // 调用的位置决定了什么时候执行
    console.log('执行一次')
  })
}
```

<br/>

- :question:&nbsp;问题：多次使用useSingleton，产生多个useRef怎么办

<br/><br/>

## class组件和函数组件共存问题

https://zhuanlan.zhihu.com/p/98554943



<br/><br/>

## 保证状态一致性

<br/>

### state最小化

<br/>

某些数据能从state、prop中计算得到，那么就在使用时去计算，而不要存在state里面。

- :chestnut:&nbsp;例子：
  - 搜索框+列表
  
    ```tsx
    // 三个状态：列表数据prop、输入框关键字state、搜索结果
    // 不用维护搜索结果
    const Demo = ({data})=>{
      const [searchKey, setSearchKey] = useState('')
      const filtered = useMemo(()=>{
        return data.filter(item=>{
          return item.title.toLowerCase().includes(searchKey.toLowerCase())
        })
      },[data, searchKey])
      const handleSearchChange = useCallback(evt=>{
        const key = evt.target.value
        setSearchKey(key)
      })
    }
    ```
    
    

<br/>

### 避免中间状态,确保唯一数据源

<br/>

<div align='center'><img src='../../../../assets/images/唯一数据源.png'/></div>

- :chestnut:&nbsp;<u>例子</u>：

  - 搜索框+列表+搜索关键字同步在浏览器url中

    ```tsx
    import getQuery from './getQuery'
    import history from './history'
    const Demo = ({data})=>{
      // 初始化时关键字从url的query中取
      const [searchKey, setSearchKey] = useState(getQuery('key'))
      const filtered = useMemo(()=>{
        return data.filter(item=>{
          return item.title.toLowerCase().includes(searchKey.toLowerCase())
        })
      },[data, searchKey])
      const handleSearchChange = useCallback(evt=>{
        const key = evt.target.value
        setSearchKey(key)
        // 当搜索框输入变化时，不仅要更新关键字state，还要改变url的query
        history.push(`/list?key=${key}`)
      })
    }
    /**
    * 一致性问题漏洞：从url的query中获得关键字state只在第一次mounting时发生，后续由onchange维持一致
    * 而中途如果其他原因导致url的query变化，关键字state不会变，一致性被破坏
    */
    // 上述，数据源有两个：用户输入 + 浏览器url的query
    // 将url的query作为唯一数据源
    import { useSearchParam } from "react-use";
    const Demo = ({data})=>{
      const searchKey = useSearchParam("key") || ""
      const handleSearch = useCallback(evt=>{
        window.history.pushState(
          {},
          '',
          `${window.location.pathname}?key=${evt.target.value}`
        )
      })
      ......
    }
    ```

    :question:&nbsp;<u>问题</u>：

    - 为什么使用 ```useSearchParam``` 这个hook？这个hook内部是如何实现的？

      > 由于 hisgory.pushState 不会触发⻚⾯重新渲染，也不会导致组件更新，所以，默认的 userSearchParam 
      >
      > s 只会获取第⼀次的 URL 上的查询字符串。因此，为了解决这个问题，可以通过监听 pushstate、replac 
      >
      > eState 等事件，对状态进⾏同步。 
      >
      >  history API 是⽐较特别的，只能⽤ patch 的⽅法来监听 url 变化。

    

<br/>

<br/>

## 向服务器端发送请求

<br/>

### [封装自定义Hooks](#自定义Hooks)

<br/>

### 多个API调用如何处理并发串行请求

<br/>

React的本质是状态驱动UI，所以当状态变化时触发请求。

<br/>

- :chestnut:&nbsp;<u>例子</u>：

  - （article id）评论列表并发请求、文章内容&nbsp;:point_right: <br/>（writer id）作者信息串行请求

    思路：

    ```tsx
    // 并发获取⽂章和评论列表 
    const [article, comments] = await Promise.all([ fetchArticle(articleId), fetchComments(articleId) ]); 
    // 得到⽂章信息后，通过 writerId 获取⽤⼾信息 
    const user = await fetchUser(article.userId);
    ```

    但是！！React函数组件是个同步的函数，没办法直接使用await。请求需要通过副作用触发：

    ```tsx
    // 自定义Hooks useUser
    export default (id)=>{
      const [data, setData] = useState(null)
      const [loading,setLoading] = useState(false)
      const [error, setError] = useState(null)
      useEffect(()=>{
        if(!id) return // 只有有id时才会发请求
        setLoading(true)
        setData(null)
        setError(false)
        fetch(`/users/${id}`).then(res=>{
          setLoading(false)
          setData(res)
        }).catch(err=>{
          setLoading(false)
          setError(err)
        })
      },[id])
      return {loading, data, error}
    }
    // 自定义Hooks useArticle
    // useComment 同理
    export default (id)=>{
      const [data, setData] = useState(null)
      const [loading,setLoading] = useState(false)
      const [error, setError] = useState(null)
      useEffect(()=>{
        setLoading(true)
        setData(null)
        setError(false)
        fetch(`/articles/${id}`).then(res=>{
          setLoading(false)
          setData(res)
        }).catch(err=>{
          setLoading(false)
          setError(err)
        })
      },[id])
      return {loading, data, error}
    }
    // 组件内使用
    const Demo = (id)=>{
      const { data: article, error, loading } = useArticle(id)
      const { data: comments } = useComment(id)
      const { data: user } = useUser(article?.userId)
      if (error) return 'failed'
      if (!article || loading) return 'loading'
      return ......
    }
    ```
    
    

<br/><br/>

## 函数组件设计模式:复杂条件渲染场景

<br/>

### 容器模式:按条件执行Hooks

<br/>

- :cake:&nbsp;<u>场景</u>：

  Hooks 在 if()...return... 之后使用会报错。因为**Hooks必须被执行到**。

  ```tsx
  const UserInfoModal = ({ visible, userId, ...rest })=>{ 
    // 当 visible 为 false 时，不渲染任何内容 
    if (!visible) return null
    // 这⼀⾏ Hook 在可能的 return 之后，会报错！ 
    const { data, loading, error } = useUser(userId)
    return ( <Modal visible={visible} {...rest}>xxx</Modal> ) }
  ```

- :white_check_mark:  <u>solution</u>：

  - 将条件判断放在外层容器中
  - 在自定义Hooks中处理
  
- :chestnut:&nbsp;<u>例子</u>：

  ```tsx
  // 将条件判断放在外层容器中
  // 适用于大块的逻辑，如子组件显示与否
  const UserInforModalWrapper = ({visible, ...rest})=>{
    if(!visible) return null
    return <UserInfoModal {...rest}/> // 子组件内部不用判断了
  }
  ```

  :question:&nbsp;问题：这种方式会丧失Modal的动画效果（即Modal的visible值的变化false）

  <br/>

  ```tsx
  // 自定义Hooks
  // 适用于内部小逻辑
  const ArticleView = ({ id }) => { 
    const { data: article, loading } = useArticle(id); 
    let user = null; 
    if (article?.userId) user = useUser(article?.userId).data; 
    ......
  }
  /**
  * 解决方案：发送串行请求课题中的useUser自定义Hook
  */
  function useUser(id) { 
    const [data, setData] = useState(null)
    const [loading, setLoading] = useState(false)
    const [error, setError] = useState(null) 
    useEffect(() => {
      if (!id) return 
      ......
    })
  }
  ```

  

<br/>

### 使用```render props```模式重用UI逻辑

<br/>

- :cake:&nbsp;<u>场景</u>：Hooks 只能用作数据逻辑的重用，如何进行UI逻辑重用？

  - 文件预览，根据选中的文件类型用对应的插件预览。

- :white_check_mark:&nbsp;<u>solution</u>：借助 render props 模式，将 render 函数作为属性传递给某组件，由组件执行该函数render实际内容。

- :chestnut:&nbsp;<u>例子</u>：

  **通过 children 这个特殊的 prop 传函数**

  ```tsx
  const CounterRenderProps = ({children}) => {
    const [count, setCount] = useState(0)
    const increment = useCallback(()=>{
      setCount(count+1)
    },[count])
    const decrement = useCallback(()=>{
      setCount(count-1)
    },[count])
    return children({count, increment, decrment})
  }
  // 使用
  const Demo = ()=>{
    return 
    <CountRenderProps>
      {(count, increment, decrment)=>{
        return
        <div>
          <button onClick={increment}>+1</button>
          <span>{count}<span/>
          <button onClick={decrement}>-1</button>
        </div>
      }}
    </CountRenderProps>
  }
  ```

  <br/>

  **通过普通的 prop 传函数**

  ```tsx
  // 5行的list + 显示更多 
  // 5个span + 显示更多
  const ListWithMore = ({renderItem, datas=[], max})=>{
    const elements = datas.map((data,index)=>renderItem(data, index, datas))
    const show = elements.slice(0,max)
    const hide = elements.slice(max)
    return 
    <>
    	{show}
    	{hide.length > 0 && 
      	<Popover content={<div>{hide}</div>}>
         <span>查看更多</span>
       	</Popover>
      }
    </>
  }
  // 使用
  <ListWithMore renderItem={(item)=><span>{item.name}</span>}{...rest}></ListWithMore>
  ```

  

<br/><br/>

## 事件处理

<br/>



### React与原生事件

<br/>

React中，无论是原生DOM节点还是组件节点上绑定的，实际上所有原生事件处理函数都绑定在App根节点上的（*React 17 以前，绑定在document上*）。

由React统一监听、管理，捕获事件后再分发到具体的虚拟DOM节点上。

<br/>

- :boom:&nbsp;<u>caution</u>：
  - 原生事件和自定义事件的机制完全不一样，原生事件是浏览器的机制，而自定义事件是组件自己的行为，本质是回调函数机制

- :question:&nbsp;<u>问题</u>：

  - 为什么要绑在根节点上？

    > 1⃣️ 虚拟DOM render 时，真实DOM 未 render 到页面上，所以无法绑定事件
    >
    > 2⃣️ React 屏蔽底层事件细节，避免浏览器兼容性问题。对于React Native这种不是通过浏览器render的，能提供一致的API。

  - 为什么事件处理函数绑定在根节点上，实际真实DOM节点上事件发生时，也能触发函数执行？

    > [浏览器事件冒泡模型](??) + react根据事件的srcElement属性知道哪个节点发出



<br/>

### 自定义事件

<br/>



- :boom:&nbsp;<u>caution</u>：
  - 关于如何理解自定义事件，组件内部调用prop中的onXxx的时机xxx就是一种自定义事件。



<br/>

### 使用Hooks避免绑定事件

<br/>

```tsx
const usekey = (node)=>{
  const [key, setKey] = useState(null);
  useEffect(()=>{
    const handleKey = evt => {
      setKey(evt.keyCode)
    }
    node.addEventListener('keypress', handleKey)
    return ()=>{
      node.removeEventListener('keypress')
    }
  },[node])
}
```



<br/><br/>

## Hooks与表单

<br/>

### 受控与非受控

<br/>

受控组件有重新渲染问题，而非受控组件输⼊过程没有对应的状态变化，因此无法动态地根据⽤⼾输⼊做 UI 上的调整 。所以：**一般都是使用受控组件的**

- 受控：值由父组件传入

  ```tsx
  function MyForm() { 
    const [value, setValue] = useState('')
    const handleChange = useCallback(evt ={
      setValue(evt.target.value)}, [])
    return <input value={value} onChange={handleChange} />
  }
  ```

- 非受控：值由组件自己决定

  ```tsx
  function MyForm() { 
    const inputRef = useRef(); 
    const handleSubmit = (evt) =>{
      evt.preventDefault(); 
      // 使⽤的时候直接从 input 节点获取值
      alert("Name: " + inputRef.current.value)
    }
    return ( 
      <form onSubmit={handleSubmit}> 
        <label> Name: <input type="text" ref={inputRef} /> </label>
        <input type="submit" value="Submit" /> 
      </form> )
  }
  ```

<br/>

### Hooks简化表单元素处理

<br/>

- :cake:&nbsp;<u>场景</u>：其实表单元素处理就是：```const [value, setValue] = useState(); <input onChange={setValue}/>```。元素数量增加，这个逻辑会重复很多次。

- :white_check_mark:&nbsp;<u>solution</u>：

  将上述逻辑封装成自定义Hook

  ```tsx
  const useForm = (initValues={})=>{
    const [values, setValues] = useState(initValues)
    const setFieldValue = useCallback((name, value)=>{
      setValues(values=>({
        ...values,
        [name]:value
      }))
    },[])
    return {values, setFieldValue}
  }
  // 使用
  const {values, setFieldValue} = useForm()
  <input value={values.name} onChange={evt=>{setFieldValue('name',evt.target.value)}}/>
  <input value={values.age} onChange={evt=>{setFieldValue('age',evt.target.value)}}/>
  ```

  加上表单验证

  ```tsx
  const useForm = (initValues={}, validators)=>{
    const [values, setValues] = useState(initValues)
    const setFieldValue = useCallback((name, value)=>{
      setValues(values=>({
        ...values,
        [name]:value
      }))
      if (validators[name]) { 
        const errMsg = validators[name](value); 
        setErrors((errors) =>({
          ...errors, 
          [name]: errMsg || null, })); }
    },[])
    return {values, setFieldValue, errors}
  }
  ```

- :question:&nbsp;<u>问题</u>：

  - 想要reset功能，如何加上
  - 如何支持异步验证（如：通过服务器端 API 判断 name 是否已存在）
  - antdesign 这些框架是如何实现Form的？（antdesign 原先使用高阶组件后来用了Hooks。Formik用了render props。React Hook Form 完全基于Hooks实现，且与前面的不同，他是非受控组件方式）



<br/><br/>

## 浮动层

<br/>

- :cake:&nbsp;<u>场景</u>：

  并列的两个部分，控制同一个modal的展示与否

  <div align='center'><img src='../../../../assets/images/浮动层case.jpg'/></div>







<br/><br/>


## 引用

- [1] [ReactHooks核心原理与实战-极客时间-王沛](https://pan.baidu.com/mbox/homepage#share/type=session)
- [2] [Dan's Blog ](https://overreacted.io/a-complete-guide-to-useeffect/)
- [3] [掘金分享](https://juejin.cn/post/6844903982037467143)
- [4] [官网文档](https://zh-hans.reactjs.org/docs/hooks-reference.html)
- [5] [掘金-闭包陷阱](https://juejin.cn/post/6844904193044512782)
- [6] [从源码角度解读“跨渲染”](https://juejin.cn/post/6844904006079217672)

