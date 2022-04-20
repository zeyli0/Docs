**基本安装注意**

1，调整 `package.json` 文件，以便确保我们安装包是`私有的(private)`，并且移除 `main` 入口。这可以防止意外发布你的代码。



**loader**

在你的应用程序中，有三种使用 loader 的方式：

- 配置（推荐）：再webpack.config.js文件中指定loader
- 
- 内联：在每个import语句中显示的指定loader
- cli：在shell命令中指定他们

```javascript
// 配置
module.exports = {
    // mode: 'production',
    entry: {
        app: './src/index.js',
        pageone: './src/pageone/index.js'
    },
    output: {
        // path: path.resolve(__dirname, '/dist'),
        path: __dirname + '/dist',
        filename: '[name].js'
    },
    module: {
        rules: [
            {test: '/\.txt$/', use: 'row-loader'},
            {test: '/\.ts$/', use: 'ts-loader'},
            {test: '/\.css$/', use: [
                {loader: 'style-loader'},
                {loader: 'css-loader', options: {modules: true}}
            ]}
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({template: './src/index.html'})
    ]
};

// 内联
import Styles from 'style-loader!css-loader?modules!./styles.css'

// CLI
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'

```

![image-20210714151004331](C:\Users\li\AppData\Roaming\Typora\typora-user-images\image-20210714151004331.png)