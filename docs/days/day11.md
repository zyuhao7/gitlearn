# Day 11：解决冲突

## 学习目标

理解冲突为什么出现，学会读懂冲突标记，并能手动完成一次冲突解决。

## 核心概念

冲突不是 Git 出错了，而是 Git 在提醒你：同一个位置出现了两份不同答案，需要人来判断。

Git 很擅长自动合并不同位置的修改。比如：

- A 分支改了 `README.md` 第 3 行
- B 分支改了 `README.md` 第 20 行

这种情况通常可以自动合并。

但如果两个分支都改了同一个文件的同一行，Git 就不知道该保留哪一份：

- `main` 分支把标题改成“Git 学习笔记”
- `feature` 分支把同一行标题改成“我的 Git 练习”

这时合并就会产生冲突。

冲突标记通常长这样：

```text
<<<<<<< HEAD
main 分支内容
=======
feature 分支内容
>>>>>>> feature/demo
```

可以这样理解：

- `<<<<<<< HEAD` 到 `=======`：当前分支的内容
- `=======` 到 `>>>>>>> feature/demo`：被合并进来的分支内容
- `HEAD`：你现在所在的分支
- `feature/demo`：你正在合并过来的分支

解决冲突不是选一个按钮，而是编辑文件，让它变成你最终想要的样子。

比如冲突内容是：

```text
<<<<<<< HEAD
# Git 学习笔记
=======
# 我的 Git 练习
>>>>>>> feature/demo
```

你可以选择保留 `main` 的内容：

```text
# Git 学习笔记
```

也可以选择保留 `feature` 的内容：

```text
# 我的 Git 练习
```

也可以把两边内容合成一个新的版本：

```text
# 我的 Git 学习笔记
```

## 解决步骤

1. 执行合并后看到冲突提示。
2. 执行 `git status` 找到冲突文件。
3. 打开冲突文件。
4. 删除 `<<<<<<<`、`=======`、`>>>>>>>` 这些冲突标记。
5. 手动整理成最终想要的内容。
6. 执行 `git add <file>`，告诉 Git 冲突已经解决。
7. 执行 `git commit` 完成合并提交。

常用命令：

```bash
git status
git add README.md
git commit
```

如果你不想继续这次合并，可以取消：

```bash
git merge --abort
```

取消后，仓库会回到合并前的状态。

## 你应该看到

出现冲突时，合并命令会明确告诉你哪几个文件有冲突：

```text
$ git merge feature/conflict-demo
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

这时 `git status` 会把这些文件列在未合并列表里：

```text
$ git status
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   README.md
```

按步骤改完文件并 `git add README.md` 后，`git status` 里这个文件会变成 `Changes to be committed`。执行 `git commit` 完成合并提交：

```text
$ git commit
[main 7c8d9e0] Merge branch 'feature/conflict-demo'
```

如果中途执行 `git merge --abort`，`git status` 会回到合并前的干净状态，冲突文件里的标记也随之消失。

## 今日练习

1. 在两个分支分别修改 `README.md` 的同一行。
2. 尝试合并制造冲突。
3. 手动解决冲突并提交。

参考流程：

```bash
git switch main
git switch -c feature/conflict-demo
```

在 `feature/conflict-demo` 分支修改 `README.md` 的第一行并提交：

```bash
git add README.md
git commit -m "docs: update title from feature"
```

切回 `main`，修改同一行并提交：

```bash
git switch main
git add README.md
git commit -m "docs: update title from main"
```

尝试合并：

```bash
git merge feature/conflict-demo
```

如果出现冲突，打开文件，整理最终内容，然后：

```bash
git add README.md
git commit
```

## 检查点

你应该知道：

- 冲突通常发生在两个分支修改了同一个位置
- `HEAD` 表示当前分支
- 冲突标记必须删除
- 解决冲突的关键是整理出正确的最终内容
- `git add` 表示告诉 Git：这个文件的冲突已经解决
