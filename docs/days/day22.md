# Day 22：理解 HEAD

## 学习目标

理解 `HEAD` 表示你当前所在的位置，以及它和分支、提交之间的关系。

## 核心概念

`HEAD` 是 Git 里的“当前位置指针”。

多数时候，`HEAD` 指向当前分支，当前分支再指向最新提交：

```text
A---B---C  main
          ^
          HEAD
```

更准确地说是：

```text
HEAD -> main -> C
```

也就是说，你提交一次后，`main` 会前进，`HEAD` 仍然跟着 `main`。

## 查看 HEAD

常用命令：

```bash
git log --oneline --decorate -3
```

你可能看到：

```text
abc1234 (HEAD -> main, origin/main) update readme
```

这表示：

- 当前提交是 `abc1234`
- `HEAD` 正指向 `main`
- `main` 和 `origin/main` 当前在同一个提交上

也可以直接查看：

```bash
git symbolic-ref --short HEAD
```

如果你在普通分支上，它会输出类似：

```text
main
```

## HEAD~1 是什么意思

很多命令里会看到：

```bash
HEAD~1
HEAD~2
```

它们表示从当前位置往前数：

| 写法 | 含义 |
|---|---|
| `HEAD` | 当前提交 |
| `HEAD~1` | 当前提交的上一个提交 |
| `HEAD~2` | 当前提交往前两个提交 |

例如：

```text
A---B---C  main
        ^
        HEAD
```

此时：

- `HEAD` 是 `C`
- `HEAD~1` 是 `B`
- `HEAD~2` 是 `A`

## detached HEAD 是什么

正常情况下，你在分支上：

```text
HEAD -> main -> C
```

如果你直接切到某个 commit：

```bash
git switch --detach <commit-id>
```

就会变成：

```text
HEAD -> B
main -> C
```

这叫 detached HEAD，意思是 `HEAD` 没有指向某个分支，而是直接指向一个提交。

detached HEAD 适合临时查看历史版本，但不适合直接长期开发。

如果你在 detached HEAD 状态下做了修改并提交，建议立刻创建分支保存：

```bash
git switch -c feature/save-detached-work
```

## HEAD 常见用法

查看上一次提交：

```bash
git show HEAD~1
```

撤销最近一次提交但保留改动：

```bash
git reset --soft HEAD~1
```

比较当前文件和上一次提交：

```bash
git diff HEAD~1
```

## 你应该看到

`git log --oneline --decorate -3` 会把 `HEAD` 指向哪里直接标在提交后面：

```text
$ git log --oneline --decorate -3
abc1235 (HEAD -> main, origin/main) update readme
def4567 add notes
789abcd init project
```

进入 detached HEAD 时，Git 会先给一段警告，最后一行告诉你现在停在哪：

```text
$ git switch --detach def4567
Note: switching to 'def4567'.

You are in 'detached HEAD' state. ...
HEAD is now at def4567 add notes
```

这时 `git status` 显示 `HEAD detached at def4567`，而不是某个分支名。切回分支后一切恢复正常：

```text
$ git switch main
Switched to branch 'main'
```

## 今日练习

1. 执行：

```bash
git log --oneline --decorate -3
```

2. 切换到另一个分支，再查看 `HEAD`。
3. 使用 `git show HEAD~1` 查看上一次提交。
4. 找一个历史提交，尝试进入 detached HEAD：

```bash
git switch --detach <commit-id>
```

5. 看完后切回 main：

```bash
git switch main
```

## 检查点

你应该知道：

- `HEAD` 表示当前所在位置
- 普通情况下是 `HEAD -> branch -> commit`
- `HEAD~1` 表示当前位置的上一个提交
- detached HEAD 是直接站在某个提交上，不在分支上
