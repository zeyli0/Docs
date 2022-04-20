`npm i babel-loader @babel/core @babel/preset-env -D`

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [ //预设
              '@babel/preset-env' 
            ],
            plugins:[
              // 转es7的语法
              ["@babel/plugin-proposal-decorators", { "legacy": true }],
              ["@babel/plugin-proposal-class-properties", { "loose" : true }]
            ]
          }
        },
        exclude: /node_modules/
      }
    ]
  }
}
```

### 其他不兼容的高级语法

```css
使用 @babel/polyfill
```