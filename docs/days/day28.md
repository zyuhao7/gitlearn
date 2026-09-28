# Day 28：常见协作规范

## 学习目标

理解团队为什么需要 Git 协作规范，并掌握几个最常见、最实用的规则。

## 核心概念

协作规范不是为了增加形式感，而是为了减少这些问题：

- 两个人同时改 main，互相覆盖
- 临时文件、密钥被提交
- 分支名字看不出用途
- 提交太乱，review 很困难
- 线上问题不知道从哪里回退

好的规范可以让团队更容易判断：谁在做什么、改动是否安全、出了问题怎么找回。

## 主分支规则

常见约定：

- `main` 保持稳定
- 不直接在 `main` 上开发大功能
- 新功能从 `feature/*` 分支开发
- 修复问题用 `fix/*` 或 `hotfix/*`
- 合并前先更新本地 main

推荐流程：

```bash
git switch main
git pull origin main
git switch -c feature/user-login
```

## 分支命名规范

分支名最好一眼能看出用途。

常见格式：

```text
feature/user-login
fix/readme-typo
hotfix/payment-error
docs/git-guide
chore/update-deps
```

建议：

- 用英文小写
- 用 `-` 分隔单词
- 前缀说明类型
- 不要用 `test`、`new`、`mybranch` 这种看不出用途的名字

## 提交前不要带入无关文件

提交前先看状态：

```bash
git status
```

再看具体差异：

```bash
git diff
git diff --cached
```

只暂存本次需要的文件：

```bash
git add docs/days/day28.md
```

不要习惯性无脑：

```bash
git add .
```

`git add .` 很方便，但也容易把临时文件、调试文件、无关修改一起提交进去。

## 不要提交敏感信息

不要提交：

- 密码
- API Key
- Token
- `.env`
- 私钥文件
- 公司内部地址或账号

如果不小心提交了敏感信息，不能只删除文件再提交。因为密钥已经进了历史记录，应该立刻让密钥失效并重新生成。

## 保持一次提交只做一件事

不推荐：

```text
docs: update guide and fix login bug and change config
```

推荐拆开：

```text
docs: update git collaboration guide
fix: correct login validation
chore: adjust local config example
```

这样 review、回退、排查问题都会更容易。

## 合并前先同步 main

准备合并前，先让自己的分支跟上 main：

```bash
git switch main
git pull origin main
git switch feature/user-login
git rebase main
```

如果团队不使用 rebase，也可以用：

```bash
git merge main
```

关键不是必须用哪一个，而是合并前要知道 main 有没有新变化。

## 常见团队约定

| 事项 | 常见做法 |
|---|---|
| 主分支 | `main` 保持可用 |
| 功能分支 | `feature/*` |
| 修复分支 | `fix/*` 或 `hotfix/*` |
| 提交信息 | 使用 `type: description` |
| 合并方式 | PR review 后合并 |
| 敏感文件 | 进入 `.gitignore`，不能提交 |

## 你应该看到

提交前 `git status` 应该只列出你这次确实要提交的文件：

```text
$ git status
On branch feature/user-login
Changes to be committed:
        modified:   docs/days/day28.md

Untracked files:
        local-notes.md
```

`local-notes.md` 出现在未跟踪列表里，说明它没被 `git add`，也就不会进入这次提交。这就是“不要无脑 `git add .`”想达到的效果。

## 今日练习

1. 从 main 创建一个符合规范的分支：

```bash
git switch main
git switch -c docs/collaboration-practice
```

2. 修改一个文档文件。
3. 用 `git status` 确认只改了预期文件。
4. 只暂存本次文件：

```bash
git add <file>
```

5. 用清晰提交信息提交：

```bash
git commit -m "docs: practice collaboration rules"
```

## 检查点

你应该知道：

- 规范的目标是降低协作成本
- main 应该保持稳定
- 分支名要能说明用途
- 提交前要检查 diff，避免带入无关文件
- 敏感信息不能提交进 Git 历史
