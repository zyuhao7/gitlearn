# Day 27：写好提交信息

## 学习目标

让提交历史更容易阅读。

## 核心概念

提交信息应该说明这次提交做了什么。清晰的提交历史能帮助排查问题和做代码审查。

## 推荐格式

```text
type: short description
```

常见 type：

- `feat`：新功能
- `fix`：修复问题
- `docs`：文档
- `refactor`：重构
- `test`：测试
- `chore`：杂项

## 示例

```bash
git commit -m "docs: add git branch guide"
git commit -m "fix: correct login validation"
```

## 你应该看到

按 `type: description` 格式写提交信息后，`git log --oneline` 看起来整齐很多：

```text
$ git log --oneline
c3d4e5f docs: add git branch guide
b2c3d4e feat: add example file
a1b2c3d init project
```

一眼就能看出哪次改了文档、哪次加了功能。

## 今日练习

1. 修改文档并使用 `docs:` 提交。
2. 新增一个示例文件并使用 `feat:` 提交。
3. 用 `git log --oneline` 查看效果。

## 检查点

你应该知道：好提交信息应该让别人不用打开代码也能大致知道改了什么。

