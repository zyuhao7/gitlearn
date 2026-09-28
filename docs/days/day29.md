# Day 29：排查问题

## 学习目标

学会用 Git 历史记录回答几个排查问题时最常见的问题：

- 这行代码是谁改的？
- 这个文件最近发生了什么变化？
- 某个提交到底改了什么？
- 问题是从哪一次提交开始出现的？

## 核心概念

Git 不只用来提交代码，也能帮助你复盘项目历史。

排查问题时，不要只靠猜。先让 Git 告诉你事实。

## 查看某个文件的历史

查看某个文件经历过哪些提交：

```bash
git log -- README.md
```

更简洁一点：

```bash
git log --oneline -- README.md
```

如果想看每次提交具体改了什么：

```bash
git log -p -- README.md
```

`-p` 会显示 patch，也就是具体 diff。

## 查看某次提交改了什么

先找到 commit id：

```bash
git log --oneline
```

再查看提交详情：

```bash
git show <commit-id>
```

只看文件列表：

```bash
git show --stat <commit-id>
```

适合快速判断这次提交影响范围。

## 查看某一行是谁改的

使用：

```bash
git blame README.md
```

它会显示每一行最后一次是谁改的、在哪个提交里改的。

如果文件很大，可以指定行号范围：

```bash
git blame -L 1,20 README.md
```

注意：`blame` 的目标不是“甩锅”，而是找到上下文。看到 commit id 后，继续用 `git show` 看当时为什么这么改。

## 搜索历史里的关键词

想知道某个关键词什么时候出现过：

```bash
git log -S "keyword"
```

例如：

```bash
git log -S "git rebase"
```

`-S` 会查找“这个字符串的出现次数发生变化”的提交，适合追踪某段代码或文字是什么时候加入/删除的。

## 用图形方式看分支历史

排查分支和合并问题时，推荐：

```bash
git log --oneline --graph --decorate --all
```

你会看到类似：

```text
* c3 docs: add day 29 troubleshooting guide
* b2 docs: expand cherry-pick guide
| * a1 feature branch work
|/
* 90 initial docs
```

这能帮助你判断：

- 当前分支在哪
- 远端分支在哪
- 分支是否分叉
- merge 或 rebase 后历史长什么样

## 找出问题从哪次提交开始

如果你知道“以前是好的，现在是坏的”，可以用 `git bisect` 二分查找。

开始：

```bash
git bisect start
git bisect bad
git bisect good <good-commit-id>
```

Git 会自动切到中间某个提交。你测试后告诉 Git：

```bash
git bisect good
```

或：

```bash
git bisect bad
```

重复几轮后，Git 会找出第一个引入问题的提交。

结束后回到原状态：

```bash
git bisect reset
```

新手不需要一开始就熟练 `bisect`，但要知道：当提交很多时，它比一个一个试快得多。

## 一个排查流程示例

假设 README 里的链接突然错了：

1. 看这个文件最近谁改过：

```bash
git log --oneline -- README.md
```

2. 查看可疑提交：

```bash
git show <commit-id>
```

3. 如果只想看链接那几行是谁改的：

```bash
git blame -L 1,40 README.md
```

4. 找到原因后，用新提交修复，而不是直接猜着改。

## 你应该看到

`git blame -L 1,20 README.md` 会在每一行前面标出最后一次改它的提交：

```text
1a2b3c4d (张伟 2026-09-01 10:12:03 +0800  1) # Git Learn in 30 Days
9f8e7d6c (李娜 2026-09-05 15:40:22 +0800  2) 这是一个面向初学者的 Git 学习项目。
```

拿到 `9f8e7d6c` 之后，继续查这次提交到底改了什么：

```text
$ git show --stat 9f8e7d6c
commit 9f8e7d6c...
Author: 李娜 <lina@example.com>
Date:   Sat Sep 5 15:40:22 2026 +0800

    docs: rewrite readme overview

 README.md | 12 ++++++------
 1 file changed, 6 insertions(+), 6 deletions(-)
```

先用 `blame` 定位到行，再用 `show` 看上下文，这是最常见的排查路径。

## 今日练习

1. 对 `README.md` 执行：

```bash
git log --oneline -- README.md
```

2. 找到一个 commit id，用：

```bash
git show --stat <commit-id>
```

3. 查看 README 前 20 行是谁改的：

```bash
git blame -L 1,20 README.md
```

4. 查看完整分支图：

```bash
git log --oneline --graph --decorate --all
```

## 检查点

你应该知道：

- `git log -- <file>` 可以看文件历史
- `git show <commit-id>` 可以看某次提交详情
- `git blame` 可以定位某一行最后是谁改的
- `git log -S` 可以搜索历史里的关键词变化
- `git bisect` 可以用二分法定位问题提交
