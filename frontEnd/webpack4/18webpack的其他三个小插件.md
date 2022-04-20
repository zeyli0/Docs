## `webpack`的其他三个小插件

1. `cleanWebpackPlugin`

每次打包之前删掉dist目录
`yarn add clean-webpack-plugin -D`

[clean-webpack-plugin](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjohnagan%2Fclean-webpack-plugin)

```js
const CleanWebpackPlugin = require('clean-webpack-plugin');

module.exports = {
  output: {
    path: path.resolve(process.cwd(), 'dist'),
  },
  plugins: [
    new CleanWebpackPlugin('./dist')
  ]
}
```

2. `copyWebpackPlugin`

一些静态资源也希望拷贝的dist中

`yarn add copy-webpack-plugin -D`

```js
const CopyWebpackPlugin = require('copy-webpack-plugin')

module.exports = {
  plugins: [
    new CopyWebpackPlugin([
      {from: 'doc', to: './dist'}
    ])
  ]
}
```

3. `bannerPlugin`内置模块

版权声明

```jsx
const webpack = require('webpack');

new 
    .BannerPlugin('hello world')
// or
new webpack.BannerPlugin({ banner: 'hello world'})
```