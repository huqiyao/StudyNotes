# useMemo





# useEffect





# 场景

- 每次props变化，products都会重新filter一下，如何优化

```tsx
export default class MineMessageNew extends React.PureComponent<Props> {
  public componentDidMount() {
    if (this.props.params && this.props.params.message_id) {
      propsActions.fetchMessage(this.props.type, this.props.params.message_id);
    } else {
      propsActions.initUiState(this.props.type, this.props.platform);
    }
  }

  public componentWillUnmount() {
    propsActions.initUiState(this.props.type, this.props.platform);
  }

  public render() {
    const { segmentations, ui, products: allProducts, dimEvents, measurements } = this.props;
    const products = __CDP__
      ? allProducts.filter((item) => item.product.platform === 'minp') // 剔除支付宝小程序
      : allProducts;
    
    ......
    
  }
}
```



