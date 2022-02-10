- git branch
查看本地分支
  
  git branch -r
  查看远程分支

  git branch -a 查看所有分支
  
  直接切换到那个分支：
  
  git checkout origin/feature
  
  
  
  如果你想在那个分支工作的话，你就需要创建一个本地分支：
  git checkout -b feature origin/feature
  
  或者使用-t参数，它默认会在本地建立一个和远程分支名字一样的分支
  git checkout -t origin/feature
  
  
  
  也可以使用fetch来做：
  git fetch origin feature:feature
  
  不过通过fetch命令来建立的本地分支不是一个track branch，而且成功后不会自动切换到该分支上
  
  你可以用gitk查看你做了些什么：
  gitk --all &



- 不带选项的时候，`git remote`命令列出所有远程主机。

  ```
  git remote 
  ```

  使用`-v`选项，可以参看远程主机的网址。

```
git remote -v
```

```
git init //初始化一个git的本地仓库

git add README.md //将我的文件装上武器，准备发射

git commit -m “first commit” //第一次发射，我的README.md 宝贝已经成功进入到本地仓库

git remote add Ceres your_first_git_address //将第一个git address命名为Ceres

git push -u Ceres master //注意咯，我要向远端木星发射了，太远了，一定要用push，很费劲的赶脚


//这时，不要动，准备再次将我的README宝贝发射到火星上去，

//但是因为我的文件已经存在与本地仓库了，因此我就不需要再多余地commit等，

//只需要将另一个远端仓库与本地仓库建立一个连接就可以了

git remote add Mars your_second_git_address //将第二个git address命名为Mars

git push -u Mars master //再次发射，目标火星上的master分支

// 注：在用 git push -u Ceres master 时也要注意这里master是你要上传的分支名称
```

```
$ git show-ref // 显示远端的相关分支；

// 修改为如下即可；

$ git push --set-upstream personal_origin D**（当前分支名）
```



error: src refspec master does not match any
error: failed to push some refs to 'github.com:zeyli0/react-todolist.git'