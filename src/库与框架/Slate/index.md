# Slate



## 简单demo

```tsx
import { Slate, withReact, Editable } form 'slate-react'
import { createEditor } form 'slate'
const Demo = ()=>{
  const editor = useMemo(createEditor(),[])
  const [value, setValue] = useState()
  // editor,value,onChange,children都是必需prop
  return 
  <Slate editor={editor} value={value} onChange={(v)=>{setValue(v)}}>
    <Editable/>
  </Slate>
}
```



## 原生selection

Transform.setSelection(editor, {anchor: ..., focus: ...})

- HTMLInputElement.setSelectionRange()
- window.getSelection()获得selection对象



## 定制快捷键



## 问题

Use compiler option '--downlevelIteration' to allow iterating of iterators

[stackoverflow-answer](https://stackoverflow.com/questions/53441292/why-downleveliteration-is-not-on-by-default)



[引用1] [原生DOM Selection API](https://developer.mozilla.org/en-US/docs/Web/API/Selection)

[引用2] [Slate Selection](https://doodlewind.github.io/slate-doc-cn/reference/slate/selection.html)

