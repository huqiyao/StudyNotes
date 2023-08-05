## 基本介绍



```tsx
<DragDropContext onDragEnd={() => {}}>
  <Droppable droppableId="Basic">
  	{provided => {
      return <div ref={provided.innerRef} {...provided.droppableProps}>
        {arr.map((item, index)=>{
          return <Draggable draggableId={item.id} index={index}>
            {provided=>{
              return <div ref={provided.innerRef}
                       {...provided.draggableProps}
                       {...provided.dragHandleProps}>{item.title}</div>
            }}
          </Draggable>
        })}
        {provided.placeholder}
      </div>
    }}
  </Droppable> 
</DragDropContext>
```



- Draggable 组件必须作为 Droppable 子组件，而 Droppable 又必须写在 DragDropContext 的作用域内。由源码也可以看出：

  

  ```tsx
  // Droppable
  export default function Droppable(props: Props) {
    const appContext: ?AppContextValue = useContext<?AppContextValue>(AppContext);
    // 如果 !appContext 则抛出错误
    // invariant 是自定义的断言函数，这种写法在 ts 项目中一般都会出现
    invariant(appContext, 'Could not find app context'); 
    ...
  }
  ```

  

  ```tsx
  // Draggable
  export default function useRequiredContext<T>(Context: ContextType<?T>): T {
    const result: ?T = useContext(Context);
    invariant(result, 'Could not find required context');
    return result;
  }
  
  export default function Draggable() {
    // Draggable 需要访问到 DragDropContext 提供的 AppContext
    const {
      contextId,
      dragHandleUsageInstructionsId,
      registry,
    } = useRequiredContext(AppContext);
    // 也需要访问到 Droppable 提供的 DroppableContext
    const { type, droppableId } = useRequiredContext(DroppableContext); 
    ...
  }
  ```

  

- Droppable 组件必传 droppableId ，

  

- Draggble 组件必传 draggableId，index







## 如何使用占位的 draggable



## 如何限定目的地
