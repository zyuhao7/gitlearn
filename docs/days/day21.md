# Day 21：使用标签

## 学习目标

学会用 Git tag 标记重要版本，例如发布版本、课程阶段完成点、可回退的里程碑。

## 核心概念

分支会移动，标签通常不移动。

例如 `main` 会随着提交不断往前走：

```text
A---B---C---D  main
```

如果你在 `B` 上打了 `v0.1.0`：

```text
A---B---C---D  main
    |
  v0.1.0
```

以后 main 继续前进，`v0.1.0` 仍然固定指向 `B`。

## 什么时候用 tag

适合：

- 发布版本：`v1.0.0`
- 课程阶段：`day10-finished`
- 重要里程碑：`before-rebase-demo`
- 回滚前留一个安全标记

不适合：

- 标记每天随手的小修改
- 代替分支做开发
- 频繁移动同一个标签

## 常用命令

创建轻量标签：

```bash
git tag v0.1.0
```

查看所有标签：

```bash
git tag
```

查看某个标签指向的提交：

```bash
git show v0.1.0
```

推送一个标签：

```bash
git push origin v0.1.0
```

推送所有本地标签：

```bash
git push origin --tags
```

新手更建议先推送指定标签，避免把本地临时标签全部推上去。

## 给历史提交打标签

如果你想给过去某个提交打标签，先找到 commit id：

```bash
git log --oneline
```

然后指定提交：

```bash
git tag v0.1.0 <commit-id>
```

## 删除标签

删除本地标签：

```bash
git tag -d v0.1.0
```

删除远端标签：

```bash
git push origin :refs/tags/v0.1.0
```

删除远端标签前要确认团队是否还在使用它。

## tag 和 branch 的区别

| 对比 | branch | tag |
|---|---|---|
| 是否会移动 | 会，提交后分支指针前进 | 通常不移动 |
| 用途 | 持续开发 | 标记某个版本 |
| 示例 | `main`、`feature/login` | `v1.0.0`、`day10-finished` |

可以这样记：

- 分支是路
- 标签是路边的里程碑

## 你应该看到

`git tag` 列出本地所有标签，`git show v0.1.0` 显示它指向的那个提交：

```text
$ git tag
v0.1.0

$ git show v0.1.0
commit 1a2b3c4...
Author: 你的名字 <你的邮箱>
Date:   Mon Sep 28 17:00:00 2026 +0800

    add readme
```

推送标签时，远端会多出一个标签引用：

```text
$ git push origin v0.1.0
To github.com:user/my-git-practice.git
 * [new tag]         v0.1.0 -> v0.1.0
```

普通 `git push` 不会自动带上标签，所以标签要单独推送。

## 今日练习

1. 用 `git log --oneline` 找到当前最新提交。
2. 给当前提交打标签：

```bash
git tag v0.1.0
```

3. 查看标签：

```bash
git tag
git show v0.1.0
```

4. 推送标签：

```bash
git push origin v0.1.0
```

## 检查点

你应该知道：

- tag 适合标记发布版本和里程碑
- tag 通常固定指向某个提交
- 分支用于继续开发，标签用于标记版本
- 推送标签需要单独执行 `git push origin <tag>`
