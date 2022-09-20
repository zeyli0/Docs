html代码：

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <a href="demo://1">打开exe文件</a>
</body>
</html>
```

demo.reg

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\demo]
"URL Protocol"=""
@="URL:demo"

[HKEY_CLASSES_ROOT\demo\shell]

[HKEY_CLASSES_ROOT\demo\shell\open]

[HKEY_CLASSES_ROOT\demo\shell\open\command]
@="\"D:\\Applications\\InstallSoftware\\HBuilderX\\HBuilderX.exe\" \"--open-url\"  \"--\" \"%1\""
```

生成的注册表demo.reg文件要执行成功才能打开

使用说明：

![img](file:///C:\Users\li\AppData\Local\Temp\ksohtml17060\wps1.jpg)