[返回目录](../git常用操作.md)

## git常用命令

1. `git branch -D <name>`：如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name> 强行删除分支`。

2. `git reflog show <childBranch>`: 查看当前的git分支是基于哪个分支创建的，运行结果如果:
```
  git reflog show <childBranch>

  32c3956 (HEAD -> currentBranch, origin/fatherBranch, fatherBranch, list) childBranch@{0}: branch: Created from fatherBranch

  childBranch 是你新建的分支。
  fatherBranch 是它的父分支，也就是来源分支
```

3. `git commit --amend`: 修改上次提交的信息

[返回目录](../git常用操作.md)
