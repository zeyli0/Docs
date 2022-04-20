## webpack 自带的优化

test.js

```jsx
let sum = (a, b) => {
  return a + b + 'sum'
}

let minus = (a, b) => {
    
  return a - b + 'minus';
}

export default {
  sum, minus
}
```

1. 使用import

index.js

```jsx
import calc from './test'

console.log(calc.sum(1, 2));
```

import在生产环境下会自动去除没有用的代码`minus`，这叫`tree-shaking`，将没有用的代码自动删除掉

index.js

```jsx
let calc = require('./test')
console.log(calc);   // es 6导出，是一个default的对象
console.log(calc.default.sum(1, 2));
```

require引入es6 模块会把结果放在default上,打包build后并不会把多余`minus`代码删除掉，不支持`tree-shaking`

2. 作用域的提升

index.js

```js
let a = 1
let b = 2
let c = 3
let d = a + b + c

console.log(d, '---------');
```

打包出来的文件

```js
console.log(r.default.sum(1,2));console.log(6,"---------")
```

在webpack中可以省略一些可以简化的代码