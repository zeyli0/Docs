### 查看 git 所有配置

```
git config --list
```

### 查看当前项目配置的 git 用户

在项目目录下输入

```
git config user.name	// 当前项目 git 用户名
git config user.email	// 当前项目 git 用户邮箱
```

设置当前项目的 git 用户
在项目目录下输入

```
git config user.name myName	// 自己的用户名
git config user.email myEmail	// 自己的邮箱
git config --list	// 查看当前项目的 git 配置信息（会先列出全局配置，最下面列出的是当前
```

#### 设置全局的 git 用户

```
git config --global user.name globalName	// 全局的用户名
git config --global user.email globalEmail	// 全局的邮箱
git config --list	// 查看配置信息
```

