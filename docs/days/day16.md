# Day 16：撤销工作区修改

## 学习目标

丢弃还没有暂存的错误修改。

## 核心概念

当你改错了文件，并且这些修改还没有 `git add`，可以用 `git restore` 恢复到上一次提交的状态。

## 常用命令

```bash
git restore README.md
```

注意：这个命令会丢弃当前工作区修改，执行前要确认这些内容确实不需要。

## 你应该看到

`git status` 会显示文件被改过，`git restore` 之后它回到干净状态：

```text
$ git status
On branch main
Changes not staged for commit:
        modified:   README.md

$ git restore README.md
$ git status
On branch main
nothing to commit, working tree clean
```

`README.md` 从“已修改”回到干净状态，就说明撤销成功了。

## 今日练习

1. 随便修改 `README.md`。
2. 执行 `git diff` 查看修改。
3. 执行 `git restore README.md`。
4. 再执行 `git status`。

## 检查点

你应该知道：`git restore <file>` 会丢弃未暂存的文件修改。

