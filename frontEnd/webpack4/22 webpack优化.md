## webpack 优化

`yarn add webpack webpack-cli html-webpack-plugin @babel/core babel-loader @babel/preset-env @babel/preset-react -D`

webpack.config.js

```js
let path = require('path')
let HtmlWebpackPlugin = require('html-webpack-plugin')


module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              '@babel/preset-env',
              '@babel/preset-react'
            ]
          }
        }
      },
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html'
    }),
  ]
}
```

## 优化：当某些包是独立的个体没有依赖

以jquery为例，`yarn add jquery -D`,它是一个独立的包没有依赖，可以在webpack配置中，配置它不再查找依赖

```js
module: {
    noParse: /jquery/, // 不用解析某些包的依赖
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              '@babel/preset-env',
              '@babel/preset-react'
            ]
          }
        }
      },
  ]
}
```

运行`npx webpack`

从2057ms -> 1946 ms

## 优化：规则匹配设置范围

```js
rules: [
  {
    test: /\.js$/,
    exclude: '/node_modules/',   // 排除
    include: path.resolve('src'),  // 在这个范围内
    use: {
      loader: 'babel-loader',
      options: {
        presets: [
          '@babel/preset-env',
          '@babel/preset-react'
        ]
      }
    }
  }
```

尽量实用`include`,不使用`exclude`,使用绝对路径

## 优化：忽略依赖中不必要的语言包

`yarn add moment webpack-dev-server -D`

忽略掉`moment`的其他语言包

```tsx
let webpack = require('webpack')

plugins: [
    new webpack.IgnorePlugin(/\.\/locale/, /moment/)
]
```

index.js

```jsx
import moment from 'moment'

let r = moment().endOf('day').fromNow()  // 距离现在多少天
console.log(r);
```

从 1.2MB 到 800kb