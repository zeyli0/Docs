想要让Git回退历史，有以下步骤：

```text
使用git log命令，查看分支提交历史，确认需要回退的版本
使用git reset --hard commit_id命令，进行版本回退
使用git push origin命令，推送至远程分支
```

快捷命令：

```text
回退上个版本：git reset --hard HEAD^ 
```

【注：HEAD是指向当前版本的指针，HEAD^表示上个版本,HEAD^^表示上上个版本】