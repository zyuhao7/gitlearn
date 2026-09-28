# Day 13：推送代码

## 学习目标

把本地提交上传到远程仓库。

## 核心概念

`push` 会把本地分支上的提交推送到远程分支。

## 常用命令

```bash
git push -u origin main
git push
```

`-u` 会建立本地分支和远程分支的默认关联，之后可以直接执行 `git push`。

## 你应该看到

第一次推送会看到对象计数，末尾提示新分支已创建、并建立了跟踪关系：

```text
$ git push -u origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 300 bytes | 300.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/your-name/your-repo.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

建立跟踪后，再执行 `git push` 输出会短得多。如果本地没有新提交，会提示：

```text
$ git push
Everything up-to-date
```

如果输出里出现 `! [rejected] main -> main (fetch first)`，说明远程有本地没有的提交，先执行 `git pull` 再推送。

## 今日练习

1. 本地提交一次修改。
2. 执行 `git push -u origin main`。
3. 打开远程仓库网页确认内容已经上传。

## 检查点

你应该知道：提交只保存到本地，推送才会同步到远程。

