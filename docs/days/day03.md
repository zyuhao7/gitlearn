# Day 03：工作区和暂存区

## 学习目标

理解为什么提交前需要先执行 `git add`。

## 核心概念

Git 的基础流程可以分成三层：

```text
工作区 -> 暂存区 -> 本地仓库
```

- 工作区：正在编辑的文件。
- 暂存区：准备进入下一次提交的改动。
- 本地仓库：已经提交保存的历史。

## 常用命令

```bash
git status
git add README.md
```

## 你应该看到

新建 `README.md` 后执行 `git status`，文件出现在未跟踪列表里：

```text
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```

执行 `git add README.md` 再执行 `git status`，同一个文件换了位置，从“未跟踪”变成“准备提交”：

```text
$ git add README.md
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README.md
```

这一步的变化，就是“已修改”和“已暂存”的区别。

## 今日练习

1. 新建 `README.md`。
2. 写入一句项目说明。
3. 执行 `git status`。
4. 执行 `git add README.md`。
5. 再次执行 `git status`。

## 检查点

你应该能区分：文件只是被修改了，和文件已经准备提交了。

