# Day 20：临时保存修改

## 学习目标

学会用 `git stash` 临时保存还不能提交的修改，解决“我正在写一半，但现在必须切分支”的问题。

## 核心概念

`stash` 可以把当前工作区和暂存区的修改先收起来，让工作区临时变干净。

可以把它理解成一个临时储物柜：

```text
工作区有改动 -> git stash -> 改动被收进 stash -> 工作区变干净
```

等你处理完别的事情，再把改动拿回来。

## 什么时候用 stash

适合：

- 代码写到一半，还不适合提交
- 需要临时切换分支
- 需要先拉取远端更新
- 想快速清空工作区做一次验证

不适合：

- 长期保存重要工作
- 代替正常提交
- 保存你完全不记得内容的修改

重要修改最好还是尽早提交到一个临时分支。

## 常用命令

保存当前修改：

```bash
git stash
```

查看 stash 列表：

```bash
git stash list
```

恢复最近一次 stash，并从列表删除：

```bash
git stash pop
```

恢复最近一次 stash，但保留在列表里：

```bash
git stash apply
```

删除某一条 stash：

```bash
git stash drop stash@{0}
```

清空所有 stash：

```bash
git stash clear
```

`clear` 很危险，执行前确认里面没有需要保留的内容。

## 给 stash 起名字

默认的 stash 名字有时候不够清楚。建议写说明：

```bash
git stash push -m "work in progress: update day20 notes"
```

查看时会更容易判断：

```bash
git stash list
```

## stash 和 commit 的区别

| 场景 | 推荐 |
|---|---|
| 临时切分支，改动还不能提交 | `git stash` |
| 一段完整的小修改 | `git commit` |
| 想长期保存一版工作 | 新建分支并提交 |
| 想让别人看到你的改动 | `git commit` + `git push` |

`stash` 是临时工具，`commit` 才是正式记录。

## 一个实际例子

你正在 `feature/login` 分支改登录功能：

```bash
git status
```

发现有未提交修改。此时线上有个 README 错别字要马上修，你可以：

```bash
git stash push -m "login form half done"
git switch main
git switch -c fix/readme-typo
```

修完并提交后，回到原分支：

```bash
git switch feature/login
git stash pop
```

你的登录功能修改就回来了。

## 可能发生冲突

`git stash pop` 也可能冲突，因为你恢复的修改和当前文件内容可能撞在一起。

处理方式和普通冲突类似：

```bash
git status
# 手动解决冲突
git add <file>
```

如果 `pop` 发生冲突，stash 通常不会自动删除。确认处理完后可以手动删除对应 stash。

## 你应该看到

`git stash` 之后工作区立刻变干净，`git stash list` 里多出一条记录：

```text
$ git stash push -m "practice stash"
Saved working directory and index state On main: practice stash

$ git status
On branch main
nothing to commit, working tree clean

$ git stash list
stash@{0}: On main: practice stash
```

`git stash pop` 之后改动回到工作区，这条记录也从列表里消失。

## 今日练习

1. 修改一个文件但不提交。
2. 执行 `git stash push -m "practice stash"`。
3. 执行 `git status`，观察工作区是否变干净。
4. 执行 `git stash list`。
5. 执行 `git stash pop` 恢复修改。
6. 再执行一次 `git status` 观察变化。

## 检查点

你应该知道：

- `stash` 适合临时保存未完成修改
- `git stash pop` 会恢复并删除最近一次 stash
- `git stash apply` 会恢复但保留 stash
- 重要工作不要长期只放在 stash 里
