## 安装前npm初始化

```
npm init -y
npm install webpack webpack-cli -D
```

```js
const path = require('path')
module.exports = {
    mode: 'development',
    entry: {
        index: '/src/index.js'
    },
    output: {
        filename: '[name].[hash:8].js',  // hash: 8只显示8位
        path: path.resolve(__dirname, 'dist'),
        publicPath: '' // 给所有打包文件引入时加前缀，包括css，js，img，如果只想处理图片可以单独在url-loader配置中加publicPath
    }
}
```

