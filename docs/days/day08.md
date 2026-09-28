# Day 08：创建分支

## 学习目标

理解分支是什么，并创建第一个分支。

## 核心概念

分支是一条独立的开发线。你可以在分支上开发新功能，不影响主分支。

## 常用命令

```bash
git branch
git branch feature/notes
git switch feature/notes
```

也可以一步创建并切换：

```bash
git switch -c feature/notes
```

## 你应该看到

`git branch` 会列出所有本地分支，当前分支前面有一个 `*`：

```text
$ git branch
* main
  feature/notes
```

创建分支本身不会切换过去。执行 `git switch feature/notes` 后会提示已经切到新分支：

```text
$ git switch feature/notes
Switched to branch 'feature/notes'
```

用 `git switch -c feature/notes` 一步创建并切换，提示会说明这是一个新建的分支：

```text
$ git switch -c feature/notes
Switched to a new branch 'feature/notes'
```

## 今日练习

1. 创建 `feature/notes` 分支。
2. 切换到这个分支。
3. 新增 `notes/branch.md` 并提交。

## 检查点

你应该能说清楚：分支让不同工作可以并行进行。

