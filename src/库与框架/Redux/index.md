# Redux



<br/><br/>

## Redux介绍

<br/>

- :+1:&nbsp;<u>优点</u>：
  - 状态共享：
    1. 跨组件的状态共享：某个组件发起请求时，将 Loading 的数据状态设为 true，另一个全局状态组件则显示 Loading 的状态。
    2. 同组件多个实例的状态共享：某个页面组件初次加载时，会发送请求拿回了一个数据，切换到另外一个页面后又返回。这时数据已经存在，无需重新加载。设想如果是本地的组件 state，那么组件销毁后重新创建，state 也会被重置，就还需要重新获取数据。
  - 状态在组件之外，使组件成为更纯粹的表现层



- :chestnut:&nbsp;<u>例子</u>：

  - 一个简单的典型例子

    ```tsx
    function counterReducer(state = initialState, action) {  
      switch (action.type) {    
        case 'counter/incremented':      
          return { value: state.value + 1 }    
        case 'counter/decremented':      
          return { value: state.value - 1 }    
        default:      
          return state
      }
    }
    
    const store = createStore(counterReducer)
    
    ReactDOM.render(<Provider store={store}>
                      <App/>
                    </Provider>, elementRoot)
    
    import { useSelector, useDispatch } from 'react-redux'
    export function Counter() {
      // 我看MA项目里不是这么用的呀
      const count = useSelector(state => state.value)
      const dispatch = useDispatch()
      return (
          <button onClick={() => dispatch({ type: 'counter/incremented' })}>
          +1</button>
      )
    }
    ```
    
    :question:&nbsp;<u>问题</u>：
    
    - 我看MA项目里不是这么用的呀：```propsActions.setEditingCampaignProperty({ name });```



- :boom:&nbsp;<u>caution</u>：

  - 需要借助react-redux工具。view与store关联需要react-redux处理

  - 通过provider组件将全局唯一的store暴露给所有的子组件

    ```tsx
    ReactDOM.render(<Provider store={store}>
                      <App/>
                    </Provider>, elementRoot)
    ```

<br/><br/>

## 异步Action

<br/>

- :cake:&nbsp;<u>场景</u>：

  ```tsx
  // 异步请求，发出3个同步action来驱动state变化
  const Demo = ()=>{
    const dispatch = useDispatch()
    const {data, loading, error} = useSelectore(state => state.list)
    useEffect(()=>{
      dispatch({type: 'FETCH_DATA_BEGIN'})
      fetch('/some-url').then(res=>{
        dispatch({ type: 'FETCH_DATA_SUCCESS', data: res })
      }).catch(err=>{
        dispatch({ type: 'FETCH_DATA_FAIL', error: err})
      })
    },[])
  }
  // 上述获取数据的过程无法重用
  // 利用redux-thunk这个中间件
  import { createStore, applyMiddleware } from 'redux' 
  import thunkMiddleware from 'redux-thunk' 
  import rootReducer from './reducer' 
  const composedEnhancer = applyMiddleware(thunkMiddleware) 
  const store = createStore(rootReducer, composedEnhancer)
  ......
  const fetchData = (url) => dispatch => {
    dispatch({type: 'FETCH_DATA_BEGIN'})
    fetch(url).then(res=>{
      dispatch({ type: 'FETCH_DATA_SUCCESS', data: res })
    }).catch(err=>{
      dispatch({ type: 'FETCH_DATA_FAIL', error: err})
    })
  }
  ......
  import fetchData from 'fetchData'
  const Demo = ()=>{
    const dispatch = useDispatch()
    const {data, loading, error} = useSelectore(state => state.list)
    useEffect(()=>{
      // 由redux-thunk这个中间件处理
      dispatch(fetchData('/xx'))
    },[])
  }
  ```

  

- :blue_book:&nbsp;<u>介绍</u>：一种 redux 的使用模式。将处理异步任务的方法包装成函数，借助 redux-thunk <u>中间件</u>*（中间件：在action到达reducer之前拦截并处理action）*来处理。

- :chestnut:&nbsp;<u>例子</u>：

  - 在自定义hooks中使用

    ```tsx
    export function useFetchAdmins() {
      const dispatch = useDispatch();
      const { admins, fetchAdminsPending, fetchAdminsError } = useSelector(
        (state) => ({
          admins: state.pluginPluginManager.home.admins,
          fetchAdminsPending: state.pluginPluginManager.home.fetchAdminsPending,
          fetchAdminsError: state.pluginPluginManager.home.fetchAdminsError,
        }),
        shallowEqual
      );
      const boundAction = useCallback(
        (...args) => {
          return dispatch(fetchAdmins(...args));
        },
        [dispatch]
      );
      useEffect(() => {
        if (!admins && !fetchAdminsPending && !fetchAdminsError) boundAction();
      },[admins, fetchAdminsPending, fetchAdminsError, boundAction]);
      return { admins, fetchAdmins: boundAction, fetchAdminsPending, fetchAdminsError };
    }
    ```

    


https://time.geekbang.org/column/article/382459