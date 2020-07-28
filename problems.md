# this在node环境中

> **node环境：**
>
> 在全局环境中，this指的是 ```module.exports``` 对象
>
> - 但在node控制台中，this指的就是Global对象
>
> 全局调用函数时，this指的是Global对象
>
> **浏览器环境：**
>
> 两种情况指的都是Window对象

```javascript
function fun(){
    this.name = 'Qiyao';
    console.log(this);
}
fun(); // 打印的this是Global对象，(见下图)
console.log(this); // {}，这个this是module.exports对象
this.age = 21;
console.log(this); // {age:21}
```

<div align='center'><img src='图片资料/node中的this.png'></div>


# Window 和 window 





# substring 和 substr

- substr(start [, length])
  - length 为0或者负数，返回空字符串
- substring(start [, end])
  - 使用start、end中的较小值作为起始点
  - start 或 end 为 NaN / 负数时，将其替换成 0



# console.log() 和 console.dir()

```javascript
function Foo(){
    console.log(1)
}
```

- 如果是```console.log(Foo)```

  <div text-align='center'><img src='./图片资料/log结果.png'></div>

- 如果是```console.dir(Foo)```

  <div text-align='center'><img src='./图片资料/dir结果.png'></div>



# 输错一次用户名和密码，就没有重输的机会，一直Authentication failed

[参考资料](https://blog.csdn.net/qq_34665539/article/details/80408282)

打开 windows 的凭据管理器，删除上次输错的记录



# 关于基本类型与构造函数实例的问题

```javascript
var str = "hello world";
console.log(str instanceof String); // false
console.log(str.__proto__ === String.prototype); // true
```



# 判空的问题

```javascript
var tags = []
console.log(tags === []) // 为什么返回false
```



# toString 与 toString()



# function的name

```javascript
// 为function及function的prototype增加name属性，并赋值
function Foo(){
    console.log(1)
}
Foo.name = 'Atong'
Foo.prototype.name = 'Qiyao'
console.dir(Foo)
```

<div text-align='center'><img src='./图片资料/problems-function的name_1.png'></div>

```javascript
// 为function及function的prototype增加nickname属性，并赋值
function Foo(){
    console.log(1)
}
Foo.nickname = 'Atong'
Foo.prototype.nickname = 'Qiyao'
console.dir(Foo)
```

<div text-align='center'><img src='./图片资料/problems-function的name_2.png'></div>

> 综上：这个是非匿名函数，自身有个内置属性```name = 函数名``` , 是不会被修改的
>
> 即使是匿名函数，也有内置属性name，只是```name = ''```，也是不能被修改的



# 使用iView的Col、Input标签报错

https://blog.csdn.net/weixin_38465623/article/details/85490353

https://blog.csdn.net/jiaqingge/article/details/80498536



# 管理员查看不到我的feature分支

https://www.cnblogs.com/zhou-chao/p/7678899.html



# vue 的 v-on:input 事件到底是什么

[参考答案](https://segmentfault.com/q/1010000009271217)



# 安装窗口逃到屏幕外边了

```Alt + space``` 进入移动状态



# 用iview的Select组件，选了之后不回显问题

```vue
<Select v-model="ruleFormData[item.prop]"
        :placeholder="item.placeholder"
        v-if="item.type == 'multiSelect'">
    <Option v-for="subitem in item.selectValue"
            :key="subitem.value"
            :value="subitem.value">
    </Option>
</Select>
```

改正：

给 ```<Option>``` 加上 ```:label="subitem.label"```



# 为什么设置crossorigin属性

当引入跨域的脚本（比如用了 apis.google.com 上的库文件）时，如果这个脚本有错误，因为浏览器的限制（根本原因是协议的规定），是拿不到错误信息的。当本地尝试使用 `window.onerror` 去记录脚本的错误时，跨域脚本的错误只会返回 ```Script error```

HTML5 新的规定，是可以允许本地获取到跨域脚本的错误信息的，但有两个条件：一是跨域脚本的服务器必须通过 `Access-Control-Allow-Origin` 头信息允许当前域名可以获取错误信息，二是网页里的 `script` 标签也必须指明 `src` 属性指定的地址是支持跨域的地址，也就是 crossorigin 属性。有了这两个条件，就可以获取跨域脚本的错误信息

[参考资料](https://www.chrisyue.com/what-the-hell-is-crossorigin-attribute-in-html-script-tag.html)



# 浮动的元素都停留在哪里

```html
<div class='container'>
    <div class='normal-box'>normal box</div>
    <div class='float-box'>float box</div>
</div>
```



# powershell yarn报错

powershell parcel 同理

[描述](https://blog.csdn.net/qq_45062261/article/details/100132489)



# IDE目录显示问题

https://www.cnblogs.com/eret9616/p/12099165.html



# 文字换行

hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh => 不换行

哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈 => 换行



# 除了第一次外，按钮点击两次后modal才出现



# 文字溢到padding



# 项目拉下来后安装包的错误与解决

```powershell
> yarn add
Missing list of packages to add to your project
```

⬇

**使用 ```npm``` 安装**

```powershell
> npm install
Unexpected end of JSON input while parsing near '...{"caniuse-lite":"^1.0'
```

⬇

清除npm缓存后重新安装

```powershell
> npm cache clean --force
```



# 为什么子组件只有两个插槽，父组件使用时填了三个元素块

```vue
// 子组件
<template>
  <Layout>
    <BasicHeader>
      <template v-slot:beforeUser>
        <slot name="headerBeforeUser"></slot> // 第一个插槽，具名插槽
      </template>
    </BasicHeader>
    <Layout>
      <Sider>
        <BasicMenu></BasicMenu>
      </Sider>
      <Content>
        <Alert v-if="browserAlert">
          浏览器版本提醒
          <span slot="desc">{{browserAlert}}</span>
        </Alert>
        <slot></slot> // 第二个插槽，匿名插槽
      </Content>
    </Layout>
  </Layout>
</template>
```



```vue
// 父组件
<template>
  <BasicLayout>
    <BasicBread/> // ② 剩下的虽然是两个代码块，但是都是用来填那个匿名插槽的
    <HeaderScreen slot="headerBeforeUser"></HeaderScreen> // ① 填第一个具名插槽
    <div> // ②
      <router-view></router-view>
    </div>
  </BasicLayout>
</template>
```



# iview的Row组件中的gutter作用

```vue
<Row :gutter='20'>
    <Col></Col>
    <Col></Col>
</Row>
⬇
<div style="margin-left:-10px;margin-right:10px">
    <div style="padding-left: 10px; padding-right: 10px;"></div>
    <div style="padding-left: 10px; padding-right: 10px;"></div>    
</div>
```



# z-index无效

https://blog.csdn.net/zhu562002124/article/details/48545609



# 改变数组对象的属性名

<div><img src='图片资料/修改对象属性名.jpg'/></div>

[参考资料](https://blog.csdn.net/alisa_lisa/article/details/95620339)



# 箭头函数的错

https://blog.csdn.net/z93701081/article/details/78933174



# vue引入后无效的问题

https://zhidao.baidu.com/question/2144542621615771268.html



# 将返回数据显示为百分比

**我的写法**：

```vue
<script>
	this.tableData = res.list.map(item => ({
      ...item,
      handlePercent: `${item.handlePercent*100}%`,
    }));
</script>
```

出现问题: ```0.0035*100 => 0.35000000000000003```

原因：

**项目中正确的写法**：

```javascript
// utils/NumberUtils
export default{
   /**
   * 求 a / b 百分数，默认保留两位小数
   * @param {Number} a 分子
   * @param {Number} b 分母
   * @param {Number} scale 小数位数
   */
  percent(a = 0, b = 1, scale = 2) {
    if (b === 0) {
      return 0;
    }
    const remainder = (a * 100) % b;
    const quotient = (a * 100) / b;
    return remainder === 0 ? quotient : Number(quotient.toFixed(scale));
  },
}
```

```vue
<script>
    import { NumU } from '@.zj/utils'
	this.tableData = res.list.map(item => ({
      ...item,
      handlePercent: `${NumU.percent(item.handlePercent, 1, 2)}%`,
    }));
</script>
```



# 比较方法的优化

```javascript
range(a){
  if(a < 0){
      a = 0;
  }else if(a > 1){
      a = 1;
  }
    return a;
}

range(a, max = 1, min = 0) {
  if(a < min){
      a = min;
  }else if(a > max){
      a = max;
  }
  return a;
 }

range(a, max = 1, min = 0){
    const ma = Math.max(min, a);
    const mi = Math.min(max, a);
    return Math.max(ma, mi);
}
```



# 媒体查询没生效问题

- @media screen and (min-width: 1920px)应写在公共样式后面

- scss结构要与前面的公共样式保持一致

  ```scss
  .chart-container{
      .chart-content{
          .part1{
              .part1_line1{} // .chart-container .chart-content .part1 .part1_line1
          }  
          .part2{}
          .img1{}
          .img2{}
          .img3{}
      }
      .bottom-content{}
  }
  @media screen and (min-width: 1920px){
      .chart-container{
      .chart-content{
          .part1_line1{} // .chart-container .chart-content .part1_line1 可能修改不了上述...part1_line1的样式
          .part2{}
          .img1{}
          .img2{}
          .img3{}
      }
      .bottom-content{}
  }
  }
  ```

  

# 安装vue-devtools

- 下载安装包 （.crx文件）

- 把安装包拖进 [chrome://extensions/](chrome://extensions/)

- 修改```C:\Users\wb-hqy757070\AppData\Local\Google\Chrome\User Data\Default\Extensions\nhdogjmejiglipccpnnnanhbledajbpd\5.3.3_0``` 下的 manifest.json文件：

  ```json
  "background": {
     "persistent": true,}
  ```

  

# 为什么vue项目没有webpack.config.js文件了

[答案](https://www.jianshu.com/p/6a57d197cd9b)

cli-3.x的没有build的配置简介了许多 如果要配置webpack 在项目根目录下创建vue.config.js 在里面进行需要的配置



# cli.vuejs.org/zh 打不开

将代理的自动检测关闭



# @代表/src，为什么没有看到其配置

因为新版的vue-cli创建项目时，隐藏了webpack.config.js文件，在其中有写到的



# li设置为 display:flex后，前面的小圆点消失



# 为什么postman的get参数可以写在请求体里面？

https://blog.csdn.net/qq_40734247/article/details/107058221



# 伪元素的content可以取什么值



# iview里render操作按钮时

```javascript
{
  title: '操作',
  key: 'action',
  render: (h, params) => {
    return h(
      'Button',
      {
        props: { type: 'text' },
        on: {
          click: () => {
            console.log(params.index);
          },
        },
      },
      '详情',
    );
  },
},
```

上面报错：```Unexpected block statement surrounding arrow body; move the returned value immediately after the '=>'```

```javascript
{
  title: '操作',
  key: 'action',
  // eslint-disable-next-line arrow-body-style
  render: (h, params) => {
    return h(
      'Button',
      {
        props: { type: 'text' },
        on: {
          click: () => {
            console.log(params.index);
          },
        },
      },
      '详情',
    );
  },
},
```



# Vscode更新之后rg.exe占用cpu过高

search.followSymlinks 改为 false

https://www.cnblogs.com/stulzq/p/8387977.html



# Vue src值怎么写

https://blog.csdn.net/qq_42991509/article/details/106806865

```vue
 <ZjIconText
      position="topIcon"
      :icon="require(`../../../../assets/imgs/risk/${riskLevelName}icon@2x.png`)"
    >
     写成 :icon="`../../../../assets/imgs/risk/${riskLevelName}icon@2x.png`" 图片不出现
      <span>{{riskLevelName}}</span>
    </ZjIconText>
```





# background-ground 与 background-image



# 关于数组的方法与浅拷贝

```javascript
export const riskBasicLevel: def.ListItem[] = [
  {
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  },
];

export const riskLevelList: def.ListItem[] = [
  ...riskBasicLevel,
{
  name: '中高风险',
  value: 'P1',
},
];
```

上述，想让中高风险排在第二位，怎么办？

第一版：

```javascript
export const riskBasicLevel: def.ListItem[] = [
  {
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  },
];
export const riskLevelList: def.ListItem[] = riskBasicList.splice(1, 0, {
  name: '中高风险',
  value: 'P1',
});

// 结果：
riskBasicLevel：[{
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中高风险',
    value: 'P1',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  }]
 
riskBasicLevel：[]
```

第二版：

```javascript
export const riskBasicLevel: def.ListItem[] = [
  {
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  },
];
export const riskLevelList: def.ListItem[] = riskBasicLevel;
riskLevelList.splice(1, 0, {
    name: '中高风险',
    value: 'P1'
})
// 结果：
riskBasicLevel、riskLevelList 都等于
 [{
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中高风险',
    value: 'P1',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  }]
```

第三版：对riskBasicLevel进行深拷贝，以免二者共享内存导致副本的改变影响

```javascript
export const riskBasicLevel: def.ListItem[] = [
  {
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  },
];
export const riskLevelList: def.ListItem[] = riskBasicLevel;
riskLevelList.splice(1, 0, {
    name: '中高风险',
    value: 'P1'
})
// 结果：
riskBasicLevel、riskLevelList 都等于
 [{
    name: '高风险',
    value: 'P0',
  },
  {
    name: '中高风险',
    value: 'P1',
  },
  {
    name: '中风险',
    value: 'P2',
  },
  {
    name: '低风险',
    value: 'P3',
  }]
```



# 关于typescript的interface

①

```typescript
// type.d.ts 
declare namespace def {
    export interface ListItem {
        name?: string;
        label?: string;
        value?: any;
        percent?: boolean;
   } 
}

// const.ts
export const topCards = (data?: { [index: string]: string | number | boolean }): def.ListItem[] => [
  {
    name: '非法经营线索数',
    value: data?.clueTotalNum,
    percent: false,
  },
  {
    name: '生成风险事件数',
    value: data?.riskTotalNum,
    percent: false,
  },
  {
    name: '风险事件处置率',
    value: data?.handleRiskPercent,
    percent: true,
  },
];
```

②

```typescript
// type.d.ts 
declare namespace def {
    export interface ListItem {
        [index:string]: any;
        name?: string;
        label?: string;
        value?: any;
   } 
}

// const.ts
export const topCards = (data?: { [index: string]: string | number | boolean }): def.ListItem[] => [
  {
    name: '非法经营线索数',
    value: data?.clueTotalNum,
    percent: false,
  },
  {
    name: '生成风险事件数',
    value: data?.riskTotalNum,
    percent: false,
  },
  {
    name: '风险事件处置率',
    value: data?.handleRiskPercent,
    percent: true,
  },
];
```

③

```typescript
// type.d.ts 
declare namespace def {
    export interface ListItem {
        name?: string;
        label?: string;
        value?: any;
   } 
}

// const.ts
interface NewListItem extends def.ListItem{
    percent?: boolean;
}
export const topCards = (data?: { [index: string]: string | number | boolean }): def.ListItem[] => [
  {
    name: '非法经营线索数',
    value: data?.clueTotalNum,
    percent: false,
  },
  {
    name: '生成风险事件数',
    value: data?.riskTotalNum,
    percent: false,
  },
  {
    name: '风险事件处置率',
    value: data?.handleRiskPercent,
    percent: true,
  },
];
```



# npm install 时出现的错误

Package require os(darwin) not compatible with your platform(win32)

https://blog.csdn.net/fabulous1111/article/details/79388841



# html: 100%根据的是谁的高度

**浏览器负责分配块级元素宽度，那么浏览器也一定可以分配高度(只是没有做)，那么浏览器本身是有宽度和高度的，设置html的height:100%，就可以获取浏览器的定高了，后面的body和div也就有了依赖。**



# 关于html、body的背景色

https://blog.csdn.net/javaloveiphone/article/details/51098972



# document是什么？

打印document，结果是该html文件的所有内容



# 为什么document.body.style.height是空的？且document.body.style对象的所有属性值都是空字符串？

我以为，这个style对象指的是body的行内style，因为没有写行内style所以都是空的