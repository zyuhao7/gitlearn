# Day 10：合并分支

## 学习目标

把分支上的成果合并回主分支。

## 核心概念

合并就是把一条分支上的提交带到另一条分支。

## 常用命令

```bash
git switch main
git merge feature/notes
```

## 你应该看到

如果 `main` 上没有新提交，合并会显示 `Fast-forward`，也就是直接把分支往前推：

```text
$ git switch main
Switched to branch 'main'

$ git merge feature/notes
Updating 1a2b3c4..5d6e7f8
Fast-forward
 notes/branch.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 notes/branch.md
```

如果 `main` 自己也有新提交，Git 会额外生成一个合并提交，提示类似 `Merge made by the 'ort' strategy.`。两种情况下合并完成后，`git log --oneline` 里都能看到 `feature/notes` 上的提交。

## 今日练习

1. 在 `feature/notes` 分支提交一个文件。
2. 切回 `main`。
3. 执行 `git merge feature/notes`。
4. 查看文件是否出现在 `main`。

## 检查点

你应该知道：合并前要确认当前所在分支，避免把方向弄反。

