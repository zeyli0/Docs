

```js
webpack.config.js

let path = require('path')
let HtmlWebpackPlugin = require('html-webpack-plugin')

let autoprefixer = require('')
let MiniCssExtractPlugin = require('mini-css-extract-plugin')
let uglify = reuqire('uglifyjs-webpack-plugin')

module.exports = {
    mode: 'development',// 'production',
    entry: {
        index: './src/index.js'
    },
    output: {
        filename: '[name].[hash:8].js',
        path: path.resolve(__dirname, 'dist')
    },
    devServer: {
        open: true,
        port: 3000,
        host: 'localhost',
        contentBase: './build',
        compress: true,
        progress: true
    },
    module: {
        rules: [
            // css-loader 解析@import这种语法
            // style-loader 将css插入到html的head中
            // loader 特点 单一
            // 多个loader需要[]
            // loader的顺序 默认从右到左执行,从下到上
            // loader 还可以写成 对象方式
            {
                test: /\.css$/,
                use: [
                    //{
                    //    loader: 'style-loader'
                    //},
                    MiniCssExtractPlugin.loader
                    'css-loader',
                    'sass-loader'
                ]
            }
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: 'main.css'
        })
        new HtmlWebpackPlugin({
            template: './src/index.html',
            filename: 'index.html',
            minify: {
                removeAttributeQuotes: true, //删除打包后的属性的双引号
                collapseWhitespace: true,
                removeomments: true
            },
            hash: true
        })
    ]
}
```

