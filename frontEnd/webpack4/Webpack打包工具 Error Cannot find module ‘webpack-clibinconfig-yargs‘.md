# Webpack打包工具 Error: Cannot find module ‘webpack-cli/bin/config-yargs‘

出现错误原因：webpack版本从@4.xx版本更新到了@5.xx版本，但是webpack-dev-server并没有进行相对应的更新，两个版本不兼容导致的这个错误

解决方法：

① 改变webpack的版本

步骤：安装之前需要将webpack和webpack-cli卸载

```
npm uninstall webpack -D
```


安装webpack

```
npm install webpack@4.39.2 -D
```


安装完成之后的版本

```
"webpack": "^4.39.2",
"webpack-cli": "^3.3.6",
"webpack-dev-server": "^3.11.0"
```


安装完成之后在终端运行

```
npm run dev
```

②改变webpack-cli的版本，其他版本不进行改变
步骤：卸载webpack-cli

```
npm uninstall webpack-cli -D
```


安装webpack-cli

```
npm instal lwebpack-cli@3.3.12 -D
```


安装完成之后的各个版本

```
"webpack": "^5.4.0",
"webpack-cli": "^3.3.12",
"webpack-dev-server": "^3.11.0"
```


安装完成之后在终端运行

```
npm run dev
```

