# Day 06：查看具体修改

## 学习目标

知道文件到底改了什么。

## 核心概念

`git status` 告诉你哪些文件变了，`git diff` 告诉你具体变了哪些行。

## 常用命令

```bash
git diff
git diff --staged
```

- `git diff`：查看工作区中还没暂存的修改。
- `git diff --staged`：查看已经暂存、还没提交的修改。

## 你应该看到

`git diff` 会用 `-` 和 `+` 标出删掉和新增的行：

```text
$ git diff
diff --git a/README.md b/README.md
index 1a2b3c4..5d6e7f8 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # Git 学习笔记
+这是新增的一行
```

执行 `git add README.md` 之后再运行 `git diff`，输出会是空的，因为工作区已经没有未暂存的改动。这时要看同一份修改，改用：

```text
$ git diff --staged
diff --git a/README.md b/README.md
index 1a2b3c4..5d6e7f8 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # Git 学习笔记
+这是新增的一行
```

两个命令看到的格式一样，区别只在于看的是“还没 add 的改动”还是“已经 add 的改动”。

## 今日练习

1. 修改 `README.md`。
2. 执行 `git diff`。
3. 执行 `git add README.md`。
4. 执行 `git diff --staged`。

## 检查点

你应该能在提交前检查自己到底准备提交了什么。

