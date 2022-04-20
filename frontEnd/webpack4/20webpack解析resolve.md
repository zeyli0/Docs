## webpack解析resolve

以`bootstrap`为例

```
npm install bootstrap  -D
```

index.js

```
import 'bootstrap/dist/css/bootstrap.css'
```

报错

```
ERROR in ./node_modules/bootstrap/dist/css/bootstrap.css 7:0
Module parse failed: Unexpected token (7:0)
You may need an appropriate loader to handle this file type.
|  * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
|  */
> :root {
|   --blue: #007bff;
|   --indigo: #6610f2;
 @ ./src/index.js 22:0-42
 @ multi (webpack)-dev-server/client?http://localhost:8081 ./src/index.js

```

这是因为`bootstrap` 4.0的css引入了新的特性，CSS Variables

安装
 `npm install postcss-custom-properties --save-dev`

配置`webpack.config.js`

```js
{
  test: /\.css$/,
  use: ['style-loader', 'css-loader', {
    loader: 'postcss-loader',
    options: {
      plugins: (loader) => [
        require("postcss-custom-properties")
      ]
    }
  }]
}
```

## 但是每次引入都很长，如何优雅引入

```js
resolve: {
  // 在当前目录查找
  modules: [path.resolve('node_modules')],
  alias: {
      'bootstrapCss': 'bootstrap/dist/css/bootstrap.css'
  }
},
```

```dart
import 'bootstrapCss'  // 在node_modules查找
```

## 省略扩展名

extensions:

```csharp
resolve: {
  // 在当前目录查找
  modules: [path.resolve('node_modules')],
  // alias: {
  //   'bootstrapCss': 'bootstrap/dist/css/bootstrap.css'
  // },
  mainFields: ['style', 'main'],   // 先用bootstrap中在package中的style,没有在用main
  // mainFiles: []  // 入口文件的名字 默认index
  extensions: ['.js', '.css', '.json']  // 当没有拓展命的时候，先默认js、次之css、再次之json
},
```