**1，在工作区修改，但未提交到暂存区（即没有add)**

```
git checkout -- 文件名
```

若想撤销工作区中所有的文件修改

```
git checkout .
```

注意：git chekcout 是让文件回到最近一次该文件git commit或git add时的状态。



```
 git config --global user.eamil "xxxxx@163.com"
 git config --global user.name "xxxxx"
 git config -l // 查看配置好的项
```

**2，工作区修改了之后，提交到了暂存区（即add),如何撤销修改？这里分俩种情况修改**

（1） 对于该文件来说，在当前分支上，你还没有commit过一次。这时候，git status后git给出提示：

![img](https://img-blog.csdnimg.cn/20190804111033961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNzEzMzky,size_16,color_FFFFFF,t_70)

是的，使用

```
git rm --cached
```

 文件名`命令来放弃该文件的暂存，这时，你用`git status`命令：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804150549849.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNzEzMzky,size_16,color_FFFFFF,t_70)

表明：test1文件不被git追踪，并且它是修改的状态，没有提交到暂存区。此时，你用git checkout -- file是没有用的。因为，前面提到过，git checkout -- file是回到最近的一次commit或者add。但是，当前你还没有一次commit过，并且，add也已经撤销了，所以Git找不到该文件在以往记录中的存在。自然没法用git checkout -- file。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804152310663.png)

git提示你：该文件在Git目前所知的文件中找不到。
此时，你可以任意的对此文件进行修改了，想好了之后，再提交到暂存区。

（2）如果你已经有了commit的记录，撤销文件。
则先：`git reset HEAD file`让该文件回到工作区的状态。
然后：`git chekcout -- file`即可
