## 配置`source-map`

`yarn add @babel/core @babel/preset-env babel-loader webpack-dev-server -D`

```
module.exports = {
  devtool: 'source-map' // 增加映射文件调试源代码
}
```

1. 源码映射 会标识错误的代码 打包后生成独立的文件 大而全 「source-map」

2. 不会呈现单独的文件 但是可以显示行和列 「eval-source-map」

3. 不会产生列有行，产生单独的映射文件 「cheap-module-source-map」

4. 不会产生文件 集成在打包后的文件中 不会产生列有行 「cheap-module-eval-source-map」

