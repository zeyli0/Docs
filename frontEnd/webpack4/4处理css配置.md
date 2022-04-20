```
npm install css-loader style-loader -D
```

```js
 module: {
     rules: [
         // css-loader   作用：用来解析@import这种语法
         // style-loader 作用：把 css 插入到head标签中
         // loader的执行顺序： 默认是从右向左（从下向上）
         // style-loader 把css插入head标签中
         // loader 功能单一
         // 多个loader 需要 []
         // 顺便默认从右到左
         // 也可以写成对象方式
         {
             test: /\.css$/,
             // use: 'css-loader'
             // use: ['style-loader', 'css-loader'],
             use: [
                 // {
                 //     loader: 'style-loader',
                 //     options: {
                 //         insertAt: 'top' // 将css标签插入最顶头  这样可以自定义style不被覆盖
                 //     }
                 // }, // css作为内部样式
                 // 这样相当于抽离成一个css文件， 如果希望抽离成分别不同的css, 需要再引入MiniCssExtractPlugin，再配置
                 MiniCssExtractPlugin.loader, // css分离出来
                 'css-loader', // css-loader 用来解析@import这种语法,
                 'postcss-loader'
             ]
         }
     ]
 }
```

