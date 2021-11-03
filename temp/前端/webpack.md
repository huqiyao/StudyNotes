# webpack

## Entry

1. entry是什么

   > 作为webpack构建内部依赖图的起点模块
   >
   > 能有多种entry point
   >
   > 默认是```./src/index.js```

   

2. entry points的配置

   > ① 单入口
   > 适合只有一个entry point，不易扩展
   >
   > ```javascript
   > module.exports = {
   > entry: './path/to/my/entry/file.js'
   > };
   > // 是缩写形式，完整的为：
   > module.exports = {
   > entry:{
   > main:'./path/to/my/entry/file.js'
   > } 
   > };
   > ```

   > ② 多入口（对象形式）
   > 适合有多个entry point的，扩展性强
   >
   > ```javascript
   > module.exports = {
   > entry: {
   > 	app: './src/app.js',
   > 	adminApp: './src/adminApp.js'
   > 	}
   > };
   > ```
   > **&Downarrow;**
   >
   > 配置多页应用

   ​	**&Downarrow;**

3. 多页应用

   > 告诉webpack需要三个独立的依赖图
   >
   > ```javascript
   > module.exports = {
   >   entry: {
   >     pageOne: './src/pageOne/index.js',
   >     pageTwo: './src/pageTwo/index.js',
   >     pageThree: './src/pageThree/index.js'
   >   }
   > };
   > ```
   >
   > 多页应用程序中，服务器返回不同的页面
   >
   > 使用 ```optimization.splitChunks``` 捆绑页面之间共享的模块



## output

1. 什么是output

   > 编译后的捆绑文件放在哪，叫什么名字
   >
   > 仅能有一种output point



2. output point的配置

   > ① 最简单情况
   >
   > ```javascript
   > module.exports = {
   >   entry: './src/index.js',
   >   output: {
   >     path: path.resolve(__dirname, 'dist'),
   >     filename: 'bundle.js'
   >   }
   > };
   > ```

   > ② 多个entry points时
   >
   > 通过占位符确保文件名称唯一
   >
   > ```javascript
   > module.exports = {
   > entry: {
   >  app: './src/app.js',
   >  search: './src/search.js'
   > },
   > output: {
   >  filename: '[name].js',
   >  path: __dirname + '/dist'
   >  // path:path.join(__dirname,'dist')
   > }
   > }; // 最后dist中有app.js, search.js
   > ```
   >
   > 



## Loaders

1. 什么是loaders

   > webpack只能理解JavaScript和json文件，
   >
   > loaders处理其他模块（处理：源代码转换。在引入时对其预编译），将其转成应用程序能使用或能加入依赖图的有效模块
   >
   > loaders是一个函数，以源文件为参数，返回结果



2. 安装loader

   > ```shell
   > npm install --save-dev css-loader
   > ```



3. 使用loaders

   > ① 在webpack.config.js中指明（recommended）
   >
   > ```javascript
   > module.exports = {
   > 	module: {
   > 		rules: [{
   >   	test: /\.css$/,
   >   	use: [{ loader: 'style-loader' },
   >            {loader: 'css-loader',
   >             options: {
   >                 modules: true // css-loader开启了css模块功能
   >             }
   >            },
   >            { loader: 'sass-loader' }]
   >      }]
   >  }
   > };
   > ```
   >
   > **order：**
   >
   > **right &rightarrow; left，bottom&rightarrow;top**
   >
   > **loader1(loader2(loader3(test.css))) &Rightarrow; return javascript**
   >
   > 

   > ② 使用import
   > ```shell
   > import Styles from 'style-loader!css-loader?modules!./styles.css';
   > ```
   >
   > 

   > ③ 使用命令行
   >
   > ```javascript
   > webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
   > ```
   >



4. 常用loaders

   - 解析ES6语法、ReactJSX：

     ```babel-loader```：转换ES6、ES7等JS语法新特性

     

     ```javascript
     // webpack.config.js
     module.exports = {
         module:{
             rules:[
                 {
                     test:/\.js$/,
                     use:'babel-loader'
                 }
             ]
         }
     }
     
     ```

     ```shell
     # 安装
     npm install @babel/core @babel/preset-env babel-loader --save-dev
     npm install react react-dom @babel/preset-react --save-dev
     ```

     ```javascript
     // .babel配置
     {
         "presets":[
             "@babel/preset-env"
         ]
     }
     ```

     

   - 解析CSS：

     ```css-loader```：加载.css文件，并转换成commonjs对象

     ```style-loader```：将样式通过```<style>```标签插入到head中

     ```less-loader```：将less转换为css

     ```shell
     npm install css-loader style-loader --save-dev
     ```

     ```shell
     npm install less less-loader --save-dev
     ```

     

   - 解析图片、字体

     ```file-loader```

     也可以

     ```url-loader```：可以设置较小资源自动base64

     

     





## Plugins

1. 介绍plugins   [与loaders比较资料](https://stackoverflow.com/questions/37452402/webpack-loaders-vs-plugins-whats-the-difference)

   > 比loaders作用更广泛
   >
   > 用于bundle文件的优化，资源管理，环境注入。作用于整个构建过程





## Mode

1. 什么是mode

   > 指定当前构建环境是development、production还是none(默认为production)，
   >
   > 从而能使用相应webpack内置函数



## Modules

1. webpack表达模块依赖性方法很多

   > import,  @import,  require,  url(...),  <img src=''/>



2. 支持很多的模块类型

   > typescript, less, sass……



## Module Resolution

1. 解析规则

   > ① 相对路径
   >
   > import/require所在目录会被认为是**上下文目录**，再加上相对路径就成绝对路径了
   >
   > ② 绝对路径
   >
   > ③ 模块路径
   >
   > ```javascript
   > import 'module'
   > import 'module/lib/file'
   > ```
   >
   > 在 ```resolve.modules``` 中指定的所有目录内搜索
   >
   > 如果路径指向一个文件：
   >
   > - 如果有扩展名：则就是此具体文件
   >
   > - 如果没有扩展名：通过 ```resolve.extensions``` 指明的文件扩展名来一一解析
   >
   > 如果指向一个文件夹（遇到文件扩展名问题则如上解决）:
   >
   > - 如果文件夹中有package.json：
   >
   >   根据 ```resolve.mainFields``` 中配置的查找，知道package.json出现第一个匹配，就确定了文件路径
   >
   > - 如果没有package.json或package.json中的main字段未返回正确路径：
   >
   >   根据 ```resolve.mainFields``` 中配置的顺序，寻找上下文目录中是否有相符的
   >
   > 



## Targets

1. 什么是target

   > webpack 能够为多种环境或 *target* 构建编译, 所以需要指明是哪一种来生成不同的构建



# 安装使用

- 新建目录
```mkdir demo```  ```cd demo```

- 生成package.json文件

  ```npm init -y```

- 安装webpack和webpack-cli

  ```npm install webpack webpack-cli --save-dev```

- 打包
  - ```./node_modules/.bin/webpack```
  - webpack



# 设置文件监听

> 文件监听？
>
> 便于开发
>
> 在原码发生变化时，自动重新构建出新的输出文件（放在磁盘里）
>
> 缺点：还是需要手动刷新浏览器以看到变化



1. package.json中设置，启动watch命令时带上```--watch```

   ```json
   "scripts":{
       "watch":"webpack --watch"
   }
   ```

2. 配置webpack.config.js中设置```watch:true```

   

# 热更新

> 便于开发
>
> 在运行时替换，添加，删除模块，而无需进行完全刷新重新加载整个页面
>
> webpack-dev-server不输出文件，而是放在内存中，构建速度更快
>
> 不适用于生产环境，只在开发环境使用



1. webpack-dev-server + HotModuleReplacementPlugin

   

2. webpack-dev-middleware

   > wdm将webpack输出的文件传输给服务器，
   >
   > 适用于灵活的定制环境





# 文件指纹

[参考资料](<https://alili.tech/archive/u3ldvzk86w/>)

> - 什么是文件指纹
>
> 打包生成的文件名后缀，通常可用作版本管理
>
> 无法与热更新一起使用，生产环境下使用



## 种类

### Hash

> 和整个项目的构建相关，只要项目文件有修改，整个项目构建的hash值就会更改；整个项目的文件缓存都将失效



### Chunkhash

> 和webpack打包的chunk有关，不同的entry会生成不同的chunkhash值
>
> 公共库和entry文件区分开，单独打包构建，就可以有不同chunkhash值
>
> 但入口文件与其依赖的css等文件打包在一个模块中,共用相同chunkhash，所以即使css未改变也不能缓存



### Contenthash

> 根据文件内容来定义hash，内容不同hash值就不同
>
> 文件内容不变，contenthash不变
>
> **未修改的静态文件文件最好使用Contenthash**



## 设置例子

### js文件

```javascript
// 修改output即可
// webpack.config,json
module.exports = {
    ……
    output:{
        filename:'[name][chunkhash:8].js'
    }
}
```



### css文件

```shell
npm install mini-css-extract-plugin --save-dev
```

```javascript
// webpack.config.js
// 使用MiniCssExtractPlugin的filename将style.cs提取成独立文件
modules:{
    rules:[
        {
            test:/.css$/,
            use:[
                //'style-loader',
                // 因为style-loader是将css文件解析后放入<style>里面
                // 与目标取css文件为独立文件不符
                MiniCssExtractPlugin.loader,
                'css-loader'
            ]
        },{
            test://,
            use:[
            	MiniCssExtractPlugin.loader,
            	'css-loader',
            	'less-loader'
            ]
        }
    ]
}
plugins:[
    new MiniCssExtractPlugin({
        filename:'[name][contentchunk:8].css'
    });
]
```



### 图片字体等文件

```javascript
// 可以在file-loader里，也可以在url-loader里
// 这里的hash不是hash这种种类，也是文件内容hash，只是一种占位符
module:{
    rules:[
        {
            test:/\.(png|svg|jpg|gif)$/,
            use:[{
                loader:'file-loader',
                options:{
                    name:'img/[name][hash:8].[ext]'
                    // 默认24位，取前8位
                    // 可以加img也可以不加
                }
            }]
        }
    ]
}
```





# 文件压缩



## js文件

> 内置了uglifyjs-webpack-plugin
>
> 且默认开启，所以无需额外配置



## css文件

```shell
npm install optimize-css-assets-webpack-plugin --save-dev
npm install cssnano --save-dev
```

```javascript
// optimize-css-assets-webpack-plugin
// cssnano css预处理器
plugins:[
    new OptimizeCssAssetsPlugin({
        assetNameRegExp:/\.css$/g,
        cssProcessor:require('cssnano')
    })
]
```





## html文件

```shell
npm install html-webpack-plugin --save-dev
```

```javascript
// 修改html-webpack-plugin，设置压缩参数
// 一个html文件对应一个配置
plugin:[
    new HtmlWebpackPlugin({
        template:path.join(__dirname,'src/index.html'), //html模板,可使用ejs语法
        filename:'index.html',// 打包出来的html文件名称
        chunks:['index'],// 生成的html需要使用的chunk
        inject:true,// true，则打包后的chunk自动注入html中
        minify:{
            html5:true,
            collapseWhitespace:true,
            minifyCss:true,
            minifyJS:true,
            removeComments:false
        }
    }),
    new HtmlWebpackPlugin({……})
]
```



# 自动清理构建产物

> 避免每次构建前手动删除dist



```shell
npm install clean-web
```

```javascript
// clean-webpack-plugin
// 默认会删除output指定的输出目录
plugins:[
    new CleanWebpackPlugin()
]
```





# 自动补齐css3前缀

> 不同内核的浏览器标准未完全统一，css加不同前缀来兼容
>
> IE---Trident => -ms
>
> firefox---Geko => -moz
>
> chrome---Webkit => -webkit
>
> opera---Presto => -o



```shell
npm install postcss-loader autoprefixer --save-dev
```

```javascript
modules:{
    rules:[
        {
            test:/.css$/,
            use:[
                MiniCssExtractPlugin.loader,
                'css-loader'
            ]
        },{
            test:/.less$/,
            use:[
            	MiniCssExtractPlugin.loader,
            	'css-loader',
            	'less-loader',
                {
                    loader:'postcss-loader',
                    options:{
                        plugins:()=>[
                            require('autoprefixer')({
                                browers:['last 2 version','>1%','ios 7']
                            })
                        ]
                    }
                }
            ]
        }
    ]
}
```





# 自动转px为rem

> 不同设备浏览器分辨率不同
>
> 用css媒体查询实现响应式布局，缺点：需写多套适配样式代码



```shell
npm install px2rem-loader --save-dev
npm install lib-flexible --save # 因为直接引用了，所以用save
# lib-flexible 解决在具体页面加载时根节点html的font-size的大小
```

```javascript
modules:{
    rules:[
        {
            test:/.less$/,
            use:[
            	MiniCssExtractPlugin.loader,
            	'css-loader',
            	'less-loader',
                {
                    loader:'postcss-loader',
                    options:{
                        plugins:()=>[
                            require('autoprefixer')({
                                browers:['last 2 version','>1%','ios 7']
                            })
                        ]
                    }
                },
                {
                    loader:'px2rem-loader',
                    options:{
                        remUnit:75, // 1rem = 75px
                        remPrecision:8 // px转换为rem时小数点位数
                    }
                }
            ]
        }
    ]
}
```

```html
<!-- src/xxx.html -->
<!-- 直接引入lib-flexible源文件，因为还不支持自动内联 -->
……
<script type='text/javascript'>
	……
</script>
……
```





# 静态资源内联



## html内联、JS内联

```shell
npm install row-loader@0.5.1 --save-dev
# row-loader读取文件，返回内容string
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!--<meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">-->
    ${require('row-loader!./meta.html)} 
    <!--因为之前配置过html-webpack-plugin，默认ejs模板引擎-->
    <title>Document</title>
</head>
<body>
    <!--初始化脚本,计算html的font-size-->
    <script>
        ${require('row-loader!babel-loader!../../node_modules/lib-flexible/flexible.js)}	</script>
</body>
</html>
```



## css内联

1. 借助style-loader

   ```json
   # 可以在option中添加配置
   modules:{
       rules:[
           {
               test:/.less$/,
               use:[
                   {
                       loader:'style-loader',
                       options:{
                           insertAt:'top',#样式插入到<head>中
                           singleton:true#将所有<style>合并成一个
                       }
                   },
               	'css-loader',
               	'less-loader',
               ]
           }
       ]
   }
   ```

   

2. 使用 ```html-inline-css-webpack-plugin```

   ```json
   # 待补充
   ```

   

# MPA打包通用方案

> 通用方案：为解决每增加一个页面都需要添加到entry中，添加一个html-webpack-plugin配置的问题
>
> 采用动态获取entry和设置html-webpack-plugin数量

```javascript
// 目录结构
+src
  +home
   -home.css
   -index.html
   -index.js
  +content
   -content.css
   -index.html
   -index.js
```

```shell
npm install glob --save-dev
```

```javascript
// webpack.config.js
const setMPA = ()=>{
    const entry = {};
    const htmlWebpackPlugins = [];
    const entryFiles = glob.sync(path.join(__dirname,'./src/*/index.js'));
    Object.keys(entryFiles).map((index)=>{
        const entryFile = entryFiles[index];
        const match = entryFile.match(/src\(.*)\/index\.js/);
        const pageName = match && match[1];
        entry[pageName] = entryFile;
        
        htmlWebpackPlugins.push(new HtmlWebpackPlugin({
        	template:path.join(__dirname,`src/${pageName}/index.html`),
        	filename:`${pageName}.html`,// 打包出来的html文件名称
        	chunks:[pageName],// 生成的html需要使用的chunk
        	inject:true,// true，则打包后的chunk自动注入html中
        	minify:{
            	html5:true,
            	collapseWhitespace:true,
            	minifyCss:true,
            	minifyJS:true,
            	removeComments:false
        	}
    	}));
        
    });
    return {
        entry,
        htmlWebpackPlugins
    }
}
const {entry, htmlWebpackPlugins} = setMPA();

module.exports = {
  entry: entry,
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name]_[chunkhash:8].js'
  },
  module:{
    rules:[
      {
        ......
      }
    ]
  },
  plugins:[
    ......    
  ].concat(htmlWebpackPlugins)  
};
```



# 使用source map

> 开发的源代码经过压缩打包等处理后，投入运行
>
> 此时报错，根据报错信息的无法确定错误原因，因为该运行代码变量结构与源代码不一致
>
> source map：信息文件，**储存着位置信息**。即，**转换后的代码的每一个位置，所对应的转换前的位置**
>
> 出错时，直接显示原始代码，而不是转换后的代码



- 使用：线上环境开启sourcemap，线上环境关闭

  为什么线上环境关闭？如果开启则会暴露业务逻辑。线上排查问题时可将sourcemap上传到错误监控系统中



```javascript
module.exports = {
  entry: entry,
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name]_[chunkhash:8].js'
  },
  module:{
    rules:[
      {
        ......
      }
    ]
  },
  plugins:[
    ......    
  ],
  devtool:'eval'
};
```

