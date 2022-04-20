## `watch` 改完代表重新打包实体

```js
module.exports = {
  watch: true,
  watchOptions: {
    poll: 1000,              // 每秒监听1000次
    aggregateTimeout: 300,   // 防抖，当第一个文件更改，会在重新构建前增加延迟
    ignored: /node_modules/  // 对于某些系统，监听大量文件系统会导致大量的 CPU 或内存占用。这个选项可以排除一些巨大的文件夹，
  },
    
}
```

