# Day 17：取消暂存

## 学习目标

把已经 `git add` 的文件从暂存区拿回来。

## 核心概念

取消暂存不会删除你的修改，只是把文件从“准备提交”状态移回工作区。

## 常用命令

```bash
git restore --staged README.md
```

## 你应该看到

`git add` 之后文件出现在“Changes to be committed”里，`git restore --staged` 之后它回到“Changes not staged”：

```text
$ git status
On branch main
Changes to be committed:
        modified:   README.md

$ git restore --staged README.md
$ git status
On branch main
Changes not staged for commit:
        modified:   README.md
```

注意文件内容一行都没丢，只是从“准备提交”变回了“还没暂存”。

## 今日练习

1. 修改 `README.md`。
2. 执行 `git add README.md`。
3. 执行 `git status`。
4. 执行 `git restore --staged README.md`。
5. 再执行 `git status`。

## 检查点

你应该能区分：撤销修改和取消暂存是两件事。

