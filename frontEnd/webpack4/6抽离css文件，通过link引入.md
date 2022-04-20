```
yarn add mini-css-extract-plugin -D
```

```js
let MiniCssExtractPlugin = require('mini-css-extract-plugin')
plugins:[
    new MiniCssExtractPlugin({
        filename: 'css/main.css'
    })
],
module: {
    rules: [
        {
            test: /\.css$/,   // css 处理
            use: [
                MiniCssExtractPlugin.loader,   // 抽离
                'css-loader', // css-loader 用来解析@import这种语法,
                'postcss-loader'
            ]
        }
    ]
}
```

