```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')
```

```js
new HtmlWebpackPlugin({
    template: 'src/index.html', // 模板文件
    filename: 'index.html', // 打包后的生成文件
    title: '浏览器头文本',
    chunksSortMode: 'manual', // 打包后chunks文件排序方式
    chunks: ['index'], // 打包后chunks名
    hash: true, // 添加hash值解决缓存问题
    minify: { // 对打包的html模板进行压缩
        removeComments: true,  // 删除属性双引号
        collapseWhitespace: true // 折叠空行变成一行
    }
})
```

[html-webpack-plugin#options](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjantimon%2Fhtml-webpack-plugin%23options)