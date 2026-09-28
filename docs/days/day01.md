# Day 01：认识 Git 和版本控制

## 学习目标

理解 Git 解决什么问题，知道“版本控制”不是背命令，而是记录项目变化。

## 核心概念

没有版本控制时，文件很容易变成：

```text
方案.docx
方案-修改版.docx
方案-最终版.docx
方案-最终真的版.docx
```

Git 的作用是记录每次修改，让你知道：

- 谁改了
- 什么时间改了
- 改了哪些内容
- 为什么要改

## 常用命令

```bash
git --version
git help
```

## 你应该看到

`git --version` 会打印本机安装的 Git 版本，版本号因人而异：

```text
$ git --version
git version 2.43.0
```

`git help` 不带参数时会列出常用命令和用法：

```text
$ git help
usage: git [-v | --version] [-h | --help] [-C <path>] ...
```

想查某个具体命令的用法，可以执行 `git help commit` 这样的命令。

## 今日练习

1. 安装 Git。
2. 执行 `git --version`。
3. 用一句话写下你理解的 Git。

## 检查点

你应该能说清楚：Git 是一个用来记录文件变化历史的工具。

