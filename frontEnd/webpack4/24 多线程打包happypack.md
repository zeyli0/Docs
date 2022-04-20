## 多线程打包`happypack`

`yarn add happypack`

`webpack.config.js`

```jsx
let Happypack = require('happypack')


rules: [
  {
    test: /\.js$/,
    exclude: '/node_modules/',
    include: path.resolve('src'),
    use: 'happypack/loader?id=js'
  },
]

plugins: [
  new Happypack({
    id: 'js',
    use: [{
      loader: 'babel-loader',
      options: {
        presets: [
          '@babel/preset-env',
          '@babel/preset-react'
        ]
      }
    }]
  })
]
```

js启用多线程，由于启用多线程也会浪费时间，因此当项目比较大的时候启用效果更好

css启用多线程

```css

{
  test: /\.css$/,
  use: 'happypack/loader?id=css'
}

new Happypack({
  id: 'css',
  use: ['style-loader', 'css-loader']
}),
```