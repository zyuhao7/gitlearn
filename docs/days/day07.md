# Day 07：忽略不需要提交的文件

## 学习目标

学会使用 `.gitignore`。

## 核心概念

不是所有文件都应该进入仓库。日志、构建产物、临时文件、密钥配置通常不应该提交。

## 示例配置

```gitignore
*.log
build/
.env
node_modules/
```

## 常用命令

```bash
git status
```

## 你应该看到

写好 `.gitignore` 后执行 `git status`，`debug.log` 不会出现在任何列表里：

```text
$ git status
On branch main

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md
```

如果 `debug.log` 之前已经被 `git add` 或提交过，`.gitignore` 就管不到它了。这时先让 Git 停止跟踪，再提交：

```bash
git rm --cached debug.log
```

## 今日练习

1. 新建 `.gitignore`。
2. 写入 `*.log`。
3. 新建 `debug.log`。
4. 执行 `git status`，确认它没有出现在待提交列表中。

## 检查点

你应该知道：`.gitignore` 只能忽略还没有被 Git 跟踪的文件。

