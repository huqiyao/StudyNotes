# React组件渲染性能



* [单个React组件的性能优化](#单个React组件的性能优化)
  * [shouldComponentUpdate控制组件是否更新](#shouldComponentUpdate控制组件是否更新)
  * [对象类型的props避免赋值时新建](#对象类型的props避免赋值时新建)
* [多个React组件的性能优化](#多个React组件的性能优化)
* [利用reselect提高数据选取的性能](#利用reselect提高数据选取的性能)



## 单个React组件的性能优化



### shouldComponentUpdate控制组件是否更新



- :cake:  <u>场景</u>：父组件更新，子组件即使 props、state 没有变化也会更新

  

- :white_check_mark:  <u>solution</u>：shouldComponentUpdate 生命周期函数默认是 return true，只要在子组件中定制shouldComponentUpdate 函数在不需要更新情况时return false 即可



- :chestnut:  <u>例子</u>：

  ```typescript
  this.state ={value: inputValue}
  <Input 
  onChange={setValue(v) + debounce(updateInputValue(v)+checkValue, 500)} 
  value={value}/>
  // setValue(v)立马改变了state，进行update
  // 0.5s后updateInputValue更新store进而传入的props改变，又重复进行update
  
  shouldComponentUpdate(nextProps, nextState){
    // 如果props的inputValue和当前state的value一致，则不再更新了
    return this.props.inputValue !== this.state.value
  }
  
  // 这样写会逻辑好像没问题，但是很奇怪吧？去除value的state，直接用props.inputValue，e.target.value一变化即更新store，debounce里只进行checkValue操作
  ```



- :rainbow:  <u>优化</u>：

  - 每个组件都写 shouldComponentUpdate，比较麻烦。有个捷径是，使用 react-redux 库的 connect

     ```tsx
     // 没有使用到store上的数据作为props则不填第一个参数，
     // 没有需要关联action的props(onXX)则不填第二个参数
     export default connect()(TodoItem) 
     // 如果不需要填第一个参数，但是需要第二个参数
     export default connect(null, mapPropsToDispatch)(TodoItem)
     ```

     

     > :question: **为什么使用 connect 可以比对 props 变化？**
     >
     > connect 过程实际产生了一个无名的 React 组件类（容器组件），改类 <u>已经定制了 shouldComponentUpdate</u> 函数来比对 props。

     

- :boom:  <u>caution</u>：
  - 如果 props 的某个属性（如 infor）是对象类型的，因为 **=== 是浅比较**（对于引用类型，只要未重新赋值，nextProps.infor === this.props.infor 总是 true ），所以即使 props.infor 内部实际上变化了也不会被检测出来



### 对象类型的props避免赋值时新建

- :chestnut:  <u>例子</u>：

  ```typescript
  // Foo组件每次mount、update，style都被赋了新的对象
  <Foo style={{color: 'red'}}><Foo/>
  
  /*改进*/
  const fooStyle = {color: 'red'} // 只在mount初始化时创建一次
  <Foo style={fooStyle}><Foo/> // style的值始终是同一个对象
  ```

  

  ```typescript
  // TodoItem组件每次mount、update，onRemove都被赋值了一个新建的匿名函数
  <TodoItem onRemove={()=>onRemoveTodo(item.id)}><TodoItem/>
    
  /*改进
  * 方法二更好，符合高内聚的要求
  */
  // 方法一、父组件传相同的函数对象给子组件，不同的子组件调用时传不同id
  <TodoItem onRemove={()=>onRemoveTodo(item.id)} id={item.id} ><TodoItem/>
  const mapDispatchToProps = (dispatch, ownProps)=> ({
    onRemoveItem: ()=>ownProps.onRemove(ownProps.id) // TodoItem组件内部可使用onRemoveItem方法
  })
  // 方法二、父组件不传给子组件函数对象，子组件自己dispatch action
  <TodoItem id={item.id} ><TodoItem/>
  const mapDispatchToProps = (dispatch, ownProps)=>{
    const {id} = ownProps;
    return {
      onRemove: dispatch(aAction(id))
    }
  }
  ```

  



## 多个React组件的性能优化







##  利用reselect提高数据选取的性能



- :cake:  <u>场景</u>：connect 的 mapStateToProps 在 store 发生变化的时候就会被调用，尽管变化的数据与组件无关。造成产生某些 prop 对应的函数重复执行。

  

- :white_check_mark:  <u>solution</u>：只要 store 中的目标 state 不变，则不重新返回 prop 对象。利用reselect的createSelector实现。



- :chestnut:  <u>例子</u>：

  ```typescript
  const mapStateToProps = (state)=>{
    const {a, b, c} = state
    return {
      a,
      b,
      c,
      uabc: u(a, b, c) // a、b、c以外的其他变化也会造成计算
    }
  }
  
  /*
  * reselect优化
  **/
  const aSelector = state => state.a
  const bSelector = state => state.b
  const cSelector = state => state.c
  const uSelector = createSelector( // 只有在a、b、c变化时才会重新执行u(a,b,c) 和 return
    [aSelector, bSelector, cSelector],
    (a, b, c) => u(a,b,c)
  )
  const mapStateToProps = (state)=>{
    const {a, b, c} = state
    return {
      a,
      b,
      c,
      uabc: uSelector(a, b, c)
    }
  }
  ```

  

  ```typescript
  const selector = createSelector(
    segmentationsService.selector,
    webhookSettingsService.selector,
    peopleVariablesSelector,
    visitorVariablesSelector,
    customEventsService.selector,
    (
      segmentations: Segmentation[],
      webhookSettings,
      peopleVariables,
      visitorVariables,
      customEvents
    ) => ({ // 只有上述参数发生变化时才会执行 serializeUserVars函数 和 retrun
      segmentations,
      webhookSettings,
      peopleVariables: serializeUserVars(peopleVariables, 'ppl'),
      visitorVariables: serializeUserVars(visitorVariables, 'vstr'),
      customEvents,
    })
  );
  ```



- :mag_right:  <u>reselect 缓存原理</u>

  

  ```typescript
  const createSelector = (selector1, selector2, resultSelector) => {
      let selectorCache1,  // selector1的结果记忆
          selectorCache2,  // selector2的结果记忆
          resultCache;     // resultSelector的结果记忆
      return (state) => {
          const subState1 = selector1(state);
          const subState2 = selector2(state);
  
          if (selectorCache1 === subState1 && selectorCache2 === subState2) {
              return resultCache;
          }
          selectorCache1 = subState1;
          selectorCache2 = subState2;     
          resultCache = resultSelector(selectorCache1, selectorCache2);
          return resultCache;
      };
  }
  ```

  
