# 30 天 Git 学习路线

这是一份总入口。每天的学习内容已经拆成独立文档，按顺序学只需要看 [30 天每日学习目录](days/README.md)。

如果你只看到 1-5 天，那是 [1-5 天基础概念速览](git-basics-day1-5.md)，不是完整课程。

## 怎么学

1. 先看路线图，了解六个阶段。
2. 打开 [每日学习目录](days/README.md)，按天阅读对应文档。
3. 每天跟着命令做一次提交，并用 `git status` 和 `git log --oneline` 复盘结果。

## 路线图

```mermaid
flowchart LR
    A["第 1-5 天<br/>基础概念"] --> B["第 6-10 天<br/>基础操作"]
    B --> C["第 11-15 天<br/>协作入门"]
    C --> D["第 16-20 天<br/>撤销与修复"]
    D --> E["第 21-25 天<br/>进阶工作流"]
    E --> F["第 26-30 天<br/>实战与规范"]
```

## 基础准备

安装 Git 后，先配置身份：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

检查配置：

```bash
git config --global --list
```
