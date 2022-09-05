gizp压缩是一种http请求优化方式，通过减少文件体积来提高加载速度，对于用户量多的网站，开启gizp压缩会大大降低服务器压力，提高加载速度，降低服务器流量成本 有两种开启方式

注意： **图片/mp3这样的二进制文件,不必压缩** 因为压缩率比较小, 比如100->80字节,而且压缩也是耗费CPU资源的. **比较小的文件不必压缩**

## 第一种方式

vue-cli生成的项目

- 安装compression-webpack-plugin

```
cnpm install compression-webpack-plugin --save-dev
vue.config.js配置Gzip压缩
configureWebpack: config => {
        // 开发环境不需要gzip
        if (process.env.NODE_ENV !== 'production') return
        config.plugins.push(
            new CompressionWebpackPlugin({
                // 正在匹配需要压缩的文件后缀
                test: /\.(js|css|svg|woff|ttf|json|html)$/,
                // 大于10kb的会压缩
                threshold: 10240
                    // 其余配置查看compression-webpack-plugin
            })
        )
    }
```

- npm run build 之后，对比之前的大小有明显的提升
- nginx配置gizp

```
listen 4300;
server_name localhost;
location / {
    root /home/static/web/wechat;
    index /index.html;
    try_files $uri $uri/ /index.html;
    gzip_static on; #静态压缩
}
```

- 第一种方式需要前端工程打包成Gzip,然后nginx开启Gzip模块

## 第二种方式

> 这种方式直接采用nginx进行Gzip化

开启gzip

```csharp
http {
    gzip on;
    复制代码
    # 启用gzip压缩的最小文件，小于设置值的文件将不会压缩
    gzip_min_length 1k;
    # gzip 压缩级别，1-9，数字越大压缩的越好，也越占用CPU时间，后面会有详细说明
    gzip_comp_level 1;
    # 进行压缩的文件类型。javascript有多种形式。其中的值可以在 mime.types 文件中找到。
    gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png application/vnd.ms-fontobject font/ttf font/opentype font/x-woff image/svg+xml;
    # 是否在http header中添加Vary: Accept-Encoding，建议开启
    gzip_vary on;
    # 禁用IE 6 gzip
    gzip_disable "MSIE [1-6]\.";
    # 设置压缩所需要的缓冲区大小     
    gzip_buffers 32 4k;
    # 设置gzip压缩针对的HTTP协议版本
    gzip_http_version 1.0;
}
```

通过启动项目查看newwork资源中的请求头是否有【Response Headers-> Content-Encoding:gzip】

