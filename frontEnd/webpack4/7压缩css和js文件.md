抽离css插件文件时可使用`optimize-css-assets-webpack-plugin`优化压缩css以及js文件

## 压缩css和js文件

```js
const UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin')
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin')
module.exports = {
    optimization: { // 优化项
        minimizer: [
            new UglifyjsWebpackPlugin({ // 优化js
                cache: true, // 是否缓存
                parallel: true  // 是否并发打包
                // sourceMap: true     // 源码映射 set to true if you want JS source maps
            }),
            new OptimizeCssAssetsPlugin() // css 的优化
        ]
    }
}
```

