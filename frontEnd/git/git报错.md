### 1.1问题`fatal: refusing to merge unrelated histories`

今天在使用Git创建项目的时候，在两个分支合并的时候，出现了下面的这个错误。

```
~/SpringSpace/newframe on  master ⌚ 11:35:56
$ git merge origin/druid
fatal: refusing to merge unrelated histories
```

这里的问题的关键在于：`fatal: refusing to merge unrelated histories`
你可能会在`git pull`或者`git push`中都有可能会遇到，这是因为两个分支没有取得关系。那么怎么解决呢？

### 1.2解决方案

在你操作命令后面加`--allow-unrelated-histories`
例如：
`git merge master --allow-unrelated-histories`

```
~/SpringSpace/newframe on  druid ⌚ 11:36:49
$ git merge master --allow-unrelated-histories
Auto-merging .gitignore
CONFLICT (add/add): Merge conflict in .gitignore
Automatic merge failed; fix conflicts and then commit the result.
```

如果你是`git pull`或者`git push`报`fatal: refusing to merge unrelated histories`
同理：
`git pull origin master --allow-unrelated-histories`
等等，就是这样完美的解决咯！



### 2.1问题`error: Your local changes to the following files would be overwritten by merge:README.md`

![image-20220211094058573](C:\Users\li\AppData\Roaming\Typora\typora-user-images\image-20220211094058573.png)

意思是本地的代码README.md会被远程代码所覆盖

### 2.2解决方法

**方法1：**如果你想保留刚才本地修改的代码，并把git服务器上的代码pull到本地

可以通过git stash将本地修改的代码暂时封存起来，先将本地代码放置stash中再pull远程代码，最后pop出来

`git stash `

`git pull origin master`

`git stash   pop`

**方法2：**如果你想完全地覆盖本地的代码，只保留服务器端代码，则直接回退到上一个版本，再进行pull：

`git reset --hard`

`git pull origin master`



### 3.1问题：解决内容冲突 : `AutoMatic merge failed；fix conflicts and then commit the result `

冲突内容：合并冲突在 README.md文件中

自动合并失败；修改冲突然后提交修改后的结果。

<<<<<<<< HEAD

​    你写的代码

===============

​    别人写的代码

\>>>>>>>>>>>>>>> e4tghhhqd128dqwenasjdqasddcvbdgffg

### 3.2解决方法:

首先先分析两个人的代码是实现相同功能而写的重复的代码,

还是各自实现的不同的功能的代码。

如果是重复代码：两个二选一删除一个，然后再把这些冲突标示符删除即可；

如果不是重复代码，两个都需要保留，只把冲突符号（红色部分）删除即可。

是自己的就保留自己的代码,

是别人的就保留别人的代码.

编译通过之后重新提交:

修改完成后：

1 git add . 将文件添加到暂存区

2 git commit -m “例如 完成了xxx功能的开发 (提交到本地仓库)"

3 git checkout xxx 切换到所开发的分支

4 git pull origin xxx 把服务器代码拉下和本地代码合并

( 注意先拉取在合并, 避免代码冲突 )

5 git merge xxx 合并自己的任务分支

6 git push  origin xxx 把合并好的最新代码推送到服务器端



### 4.2问题：树冲突

文件名修改造成的冲突，称为树冲突。

比如，a用户把文件改名为a.c，b用户把同一个文件改名为b.c，那么b将这两个commit合并时，会产生冲突。

$ git status
  added by us:  b.c
  both deleted:  origin-name.c
  added by them: a.c

如果最终确定用b.c，那么

### 4.2解决方法：

解决办法如下：

git **rm** a.c
git **rm** origin-name.c
git add b.c
git commit

执行前面两个git rm时，会告警“file-name : needs merge”，可以不必理会。

树冲突也可以用git mergetool来解决，但整个解决过程是在交互式问答中完成的，用d 删除不要的文件，用c保留需要的文件。

最后执行git commit提交即可。