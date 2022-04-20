`yarn add postcss-loader autoprefixer -D`s

```js
const autoprefixer = require("autoprefixer")
module: {
	rules: [
         {
             test: /\.css$/,
             use: [
                 {
                     loader: 'postcss-loader',
                     options: {
                         plugins: function(){
                             return autoprefixer('last 5 versions')
                         }
                     }
                 }
             ]
         }
    ]
}
```

