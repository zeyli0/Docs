​	**npm run build配置**

```
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    // "build": "webpack",  // =>  npm run build --  --config webpack.config.js
    "build": "webpack --config webpack.config.js",  // =>  npm run build
    "dev": "webpack-dev-server"
  },
  "devDependencies": {
    "webpack": "^4.39.2",
    "webpack-cli": "^3.3.12",
    "webpack-dev-server": "^3.11.0"
  }
}

```

