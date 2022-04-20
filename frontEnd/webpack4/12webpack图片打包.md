## webpack图片打包

1. js中创建
2. css中引入
3. `<img src="" />`

```
yarn add file-loader -D
```

适合一二情况

```js
module.export={
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: 'file-loader'
      }
    ]
  }
}
```

默认会内部生成一张图片到build,生成图片的路径返回回来

第一种情况: 图片地址要`import`引入，直接写图片的地址，会默认为字符串

```js
import logo from './logo.png'

let image = new Image()
image.src = logo
document.body.appendChild(image)
```

第二种情况: `css-loader`会将`css`里面的图片转为`require`的格式

```css
div {
  background: url("./logo.png");
}
```

第三种情况: 解析`html`中的`image`

```
yarn add html-withimg-loader -D
```

```js
{
  test: /\.html$/,
  use: 'html-withimg-loader'
}
```

