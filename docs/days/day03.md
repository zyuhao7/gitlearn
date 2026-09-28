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

## 常见报错

- `fatal: pathspec 'readme.md' did not match any files`：`git add` 后面的文件名跟实际文件对不上。Linux 和 macOS 区分大小写，`README.md` 和 `readme.md` 是两个文件。用 `ls` 看准文件名，或者直接敲 `git add` 再按 Tab 补全。
- `fatal: not a git repository (or any of the parent directories): .git`：当前目录不是仓库，回到 `git init` 过的目录里再执行。
- 同一个文件同时出现在 `Changes to be committed` 和 `Changes not staged for commit` 里：你在 `git add` 之后又改了这个文件。Git 暂存的是 `add` 那一刻的内容，后面的改动还在工作区。想要把最新的改动也提交，再执行一次 `git add`。

## 今日练习

1. 新建 `README.md`。
2. 写入一句项目说明。
3. 执行 `git status`。
4. 执行 `git add README.md`。
5. 再次执行 `git status`。

## 检查点

你应该能区分：文件只是被修改了，和文件已经准备提交了。

