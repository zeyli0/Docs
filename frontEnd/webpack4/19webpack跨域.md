## `webpack` 跨域

设置一个服务,由于`webpack-dev-server`内含`express`

[express](https://links.jianshu.com/go?to=https%3A%2F%2Fexpressjs.com%2Fzh-cn%2Fstarter%2Fhello-world.html)

```
server.js
```

```js
// express

let express = require('express')

let app = express();

app.get('/api/user', (res) => {
  res.json({name: 'mayufo'})
})

app.listen(3000)   // 服务端口在3000
```

写完后记得`node server.js`

访问 `http://localhost:3000/api/user` 可见内容

```
index.js
```

```js
// 发送一个请求
let xhr = new XMLHttpRequest();

// 默认访问 http://localhost:8080  webpack-dev-server 的服务 再转发给3000
xhr.open('GET', '/api/user', true);

xhr.onload = function () {
  console.log(xhr.response)
}

xhr.send();

```

webpack.config.js

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': 'http://localhost:3000'
    }
  },
}
```

## 1.如果后端给的请求没有API 「跨域」

```js
// express

let express = require('express')

let app = express();


app.get('/user', (res) => {
  res.json({name: 'mayufo'})
})

app.listen(3000)   // 服务端口在3000
```

请求已api开头, 转发的时候再删掉api

```js
devServer: {
  proxy: {
    '/api': {
      target: 'http://localhost:3000',
      pathRewrite: {'^/api': ''}
    }
  }
}
```

## 2.前端只想单纯mock数据 「跨域」

```js
devServer: {
  // proxy: {
  //     '/api': 'http://localhost:3000' // 配置一个代理
  // }
  //   proxy: {   // 重写方式 把请求代理到express 上
  //       '/api': {
  //           target: 'http://localhost:3000',
  //           pathRewrite: {'^/api': ''}
  //       }
  //   }
  before: function (app) {  // 勾子
    app.get('/api/user', (req, res) => {
      res.json({name: 'tigerHee'})
    })
  }
},
```

## 3.有服务端，不用代理, 服务端启动webpack 「跨域」

`server.js`中启动`webpack`
`yarn add webpack-dev-middleware -D`
`server.js`

```js
// express

let express = require('express')
let webpack = require('webpack')
let app = express();


// 中间件
let middle = require('webpack-dev-middleware')

let config = require('./webpack.config')


let compiler = webpack(config)


app.use(middle(compiler))

app.get('/user', (req, res) => {
  res.json({name: 'mayufo'})
})


app.listen(3000)

```

