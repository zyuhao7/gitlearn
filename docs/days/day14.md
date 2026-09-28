# Day 14：拉取远程更新

## 学习目标

获取远程仓库里的最新提交。

## 核心概念

`pull` 会把远程更新拉到本地，并尝试合并到当前分支。

## 常用命令

```bash
git pull
```

它可以粗略理解为：

```bash
git fetch
git merge
```

## 你应该看到

远程有新内容时，`pull` 会把改动拉下来并合并，末尾显示哪些文件更新了：

```text
$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/your-name/your-repo
   1a2b3c4..5d6e7f8  main       -> origin/main
Updating 1a2b3c4..5d6e7f8
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
```

如果本地已经是最新的，输出只有一行：

```text
$ git pull
Already up to date.
```

拉取后打开 `README.md`，应该能看到你在网页上改的内容。

## 今日练习

1. 在远程仓库网页修改 `README.md`。
2. 回到本地执行 `git pull`。
3. 检查本地文件是否更新。

## 检查点

你应该养成习惯：开始工作前先拉取最新代码。

