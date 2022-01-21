# Case 1

<div align='center'> <img width='200px' height='300px' src='../../assets/images/week1-editor-column.jpg'/></div>

如果我写 1 + 2✖️3 + 1✖️3 + 1✖️4 个 div，那不是很蠢，更何况有5、6……n个columns呢

那就写个 configs 吧：

```tsx
const contentConfigs = [
  { title: 'Text', icon: EditorText },
  { title: 'Button', icon: EditorButton },
  { title: 'Image', icon: EditorImage }
]

const columnConfigs = [
  { title: '1 Column', column: 1, groups: [[1]] },
  {
    title: '2 Columns',
    column: 2,
    groups: [
      [1 / 2, 1 / 2],
      [1 / 4, 3 / 4],
      [1 / 3, 2 / 3]
    ]
  },
  { title: '3 Columns', column: 3, groups: [[1 / 3, 1 / 3, 1 / 3]] }, 
  { title: '4 Columns', column: 4, groups: [[1 / 4, 1 / 4, 1 / 4, 1 / 4]] }
]

const Columns: React.FC<{}> = () => {
  return (
    <div className={styles.columns}>
      {columnConfigs.map(column => {
        return (
          <div key={column.title}>
            <div>{column.title}</div>
            {column.groups.map((item, index) => {
              return (
                <div className={styles.columnWapper} key={index} draggable>
                  <div className={styles.column}>
                    {item.map((percent, index, arr) => {
                      return (
                        <div
                          key={index}
                          style={{
                            width: `${percent * 100}%`
                          }}
                          className={classNames(styles.columnPartition, {
                            [styles.hasBorder]: arr.length > 1 && index < arr.length - 1
                          })}
                        ></div>
                      )
                    })}
                  </div>
                </div>
              )
            })}
          </div>
        )
      })}
    </div>
  )
}
```

写了 3 个嵌套的 map 😭



# Case 2

<div align='center'> <img width='400px' height='400px' src='../../assets/images/week1-editor-classname.jpg'/></div>

 如果再嵌套几个div，我就词穷了，我要找个命名的新思路