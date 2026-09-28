# Day 05：查看历史记录

## 学习目标

学会查看提交历史。

## 核心概念

Git 会按时间保存提交记录。每条提交都有一个提交编号，也叫 commit id。

## 常用命令

```bash
git log
git log --oneline
```

`git log --oneline` 更适合日常快速查看：

```text
1a2b3c4 add readme
5d6e7f8 init project
```

## 你应该看到

`git log` 默认会把每次提交的编号、作者、时间和提交信息分行展示：

```text
$ git log
commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b (HEAD -> main)
Author: Your Name <you@example.com>
Date:   Mon Sep 28 10:00:00 2026 +0800

    add readme

commit 5d6e7f8a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6
Author: Your Name <you@example.com>
Date:   Mon Sep 28 09:50:00 2026 +0800

    init project
```

同样的历史用 `git log --oneline` 就压缩成一行一条，最新的提交在最上面：

```text
$ git log --oneline
1a2b3c4 add readme
5d6e7f8 init project
```

## 常见报错

- `fatal: your current branch 'main' does not have any commits yet`：仓库里还没有任何提交，`git log` 没有东西可显示。先完成一次 `git commit`。
- `git log` 输出后画面停住退不出来：`git log` 默认调用分页器，按 `q` 退出，按空格翻页，按上下方向键逐行滚动。
- 提示 `command not found: less`：分页器缺失或被 `PAGER` 环境变量改坏了。用 `git --no-pager log --oneline` 直接打印，不加分页。

## 今日练习

1. 修改 `README.md`。
2. 再提交一次。
3. 执行 `git log --oneline`。

## 检查点

你应该能从历史里看出每次提交的顺序和提交信息。

