## Webpack

[TOC]

### 模式mode

### 入口entry

### 出口output

### loader

```
module.exports = {
	module: {
		rules: [
		{}
		]
	}
}
```

​     loader用于对模块的源代码进行转换。loader可以在import或者”加载“模块时预处理文件，loader可以将文件的从不同的语言如（Typescript)转换为JavaScript，或将内联图像转换为data url，loader甚至于能直接在js模块中直接import css文件。	

### plugins

插件目的在于解决loader无法实现的其他事，webpack插件是一个具有apply属性的JavaScript对象。apply属性会被webpack compiler调用，并且compiler对象可在整个编译生命周期访问。

