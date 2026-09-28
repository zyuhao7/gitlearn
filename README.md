# Git Learn in 30 Days

这是一个面向初学者的 Git 30 天学习项目。

它不是命令速查表，而是通过每天一个小场景，带你理解 Git 怎么记录代码变化、怎么协作、怎么回退、怎么解决冲突。

如果你刚开始学 Git，可以从每日目录按顺序学；如果你已经会基本提交，可以直接跳到分支、冲突、rebase、PR 等章节。

## 适合谁

- 刚开始学 Git 的同学
- 会用 `git add`、`git commit`，但不理解分支、冲突、rebase 的同学
- 想把 Git 用在真实项目协作中的同学

## 学习方式

每天建议花 10 到 20 分钟：

1. 先看当天概念
2. 再跟着命令操作
3. 最后完成当天练习
4. 用 `git status` 和 `git log --oneline` 复盘当天结果

## 快速入口

完整路线在这里：

[30 天 Git 学习路线](docs/git-30-days.md)

每天的内容都在这里，按顺序学只需看这一份：

[30 天每日学习目录](docs/days/README.md)

只想先过一遍前 5 天基础概念，可以看：

[1-5 天基础概念速览](docs/git-basics-day1-5.md)

## 最小准备

这个项目是纯 Markdown 学习文档，不需要安装依赖。

你只需要本机已经安装 Git。开始练习前，先配置你的身份：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

检查是否配置成功：

```bash
git config --global --list
```

## 推荐练习仓库结构

```text
my-git-practice/
  README.md
  notes/
    day01.md
    day02.md
  src/
    hello.txt
```

你可以每天在这个练习仓库里提交一次，30 天结束后会得到一条完整的 Git 学习提交记录。

## 学完以后

完成 30 天后，你应该能独立完成这些事情：

- 初始化仓库并提交代码
- 使用分支开发功能
- 推送、拉取和克隆远程仓库
- 解决冲突
- 撤销错误修改
- 使用 tag、stash、rebase、cherry-pick
- 通过 Pull Request 参与协作
