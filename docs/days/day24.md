# Day 24：整理提交记录实战

## 学习目标

学会在提交代码之前，把本地提交记录整理成别人容易阅读、容易 review、容易回退的样子。

今天不再重点解释 `rebase` 的原理，Day 23 已经讲过。今天重点是：遇到混乱提交时，具体怎么整理。

## 什么是好的提交记录

好的提交记录不是“越少越好”，而是每个提交都应该表达一个清晰的意图。

比较差的提交历史：

```text
a1 修改
b2 fix
c3 再修一下
d4 临时提交
e5 补测试
```

比较好的提交历史：

```text
a1 docs: explain rebase workflow
b2 docs: add rebase conflict examples
c3 docs: add day 24 commit cleanup practice
```

好的提交通常有几个特点：

- 一个提交只做一类事情
- 提交信息能说明“为什么改”
- 不保留明显的临时提交，例如 `fix typo`、`wip`、`再改一下`
- 相关的小修复可以合并到对应提交里
- 不相关的改动应该拆开提交

## 整理前先检查

整理提交历史前，先确认当前状态：

```bash
git status
git log --oneline --decorate -5
```

如果你担心整理错，可以先创建一个备份分支：

```bash
git branch backup/before-cleanup
```

这样即使 rebase 搞乱了，也可以回到备份分支重新来。

## 场景一：修改最近一次提交信息

如果只是最近一次提交信息写错了：

```bash
git commit --amend
```

Git 会打开编辑器，让你修改最后一次提交信息。

也可以直接写：

```bash
git commit --amend -m "docs: explain commit cleanup workflow"
```

注意：`--amend` 会生成一个新的提交，所以它也属于改写历史。

适合：

- 提交还没推送
- 或者这个分支只有你自己用

不适合：

- 已经推送到多人共享分支
- 别人已经基于这个提交继续开发

## 场景二：把漏掉的文件补进最近一次提交

比如你刚提交完才发现漏了一个文件：

```bash
git add docs/days/day24.md
git commit --amend
```

如果不想改提交信息：

```bash
git add docs/days/day24.md
git commit --amend --no-edit
```

整理前：

```text
A---B  main
    B: docs: add day 24 guide

工作区还有漏掉的 day24.md 修改
```

整理后：

```text
A---B'  main
     B': docs: add day 24 guide
```

`B'` 是新提交，里面包含原来的内容和补进去的文件。

## 场景三：合并多个零碎提交

假设你现在有 3 个本地提交：

```text
a1 docs: add day 24 outline
b2 fix typo
c3 add missing example
```

其中 `b2` 和 `c3` 都只是修补 `a1`，可以合并成一个提交。

执行：

```bash
git rebase -i HEAD~3
```

打开后可能看到：

```text
pick a1 docs: add day 24 outline
pick b2 fix typo
pick c3 add missing example
```

改成：

```text
pick a1 docs: add day 24 outline
fixup b2 fix typo
fixup c3 add missing example
```

保存后，Git 会把 `b2`、`c3` 合并进 `a1`。

整理前：

```mermaid
flowchart LR
    A["A<br/>main"] --> B["a1<br/>outline"]
    B --> C["b2<br/>fix typo"]
    C --> D["c3<br/>missing example"]
    D --> H["HEAD"]
```

整理后：

```mermaid
flowchart LR
    A["A<br/>main"] --> B["a1'<br/>完整的 Day 24 提交"]
    B --> H["HEAD"]
```

## squash 和 fixup 的区别

`squash` 和 `fixup` 都是合并到上一个提交。

区别是：

| 指令 | 作用 |
|---|---|
| `squash` | 合并内容，并让你重新编辑提交信息 |
| `fixup` | 合并内容，丢弃当前提交信息 |

如果小提交的信息还有参考价值，用 `squash`。

如果小提交只是 `fix typo`、`wip`，用 `fixup` 更干净。

## 场景四：修改历史中的某个提交信息

如果不是最后一次提交，而是前面某个提交信息写得不好：

```bash
git rebase -i HEAD~3
```

把目标提交前面的 `pick` 改成 `reword`：

```text
reword a1 docs: day 24
pick b2 docs: add examples
pick c3 docs: add exercises
```

保存后，Git 会停下来，让你重新编辑 `a1` 的提交信息。

## 场景五：删除不想要的本地提交

如果某个提交完全不需要了，可以用 `drop`。

```text
pick a1 docs: add day 24 outline
drop b2 debug temporary file
pick c3 docs: add exercise
```

保存后，`b2` 会从当前分支历史里消失。

注意：

- `drop` 会丢掉这个提交带来的改动
- 使用前确认这个提交确实不需要
- 不确定时先建备份分支

## 场景六：修改历史中的某个提交内容

如果你想修改前面某个提交的内容，用 `edit`。

先执行：

```bash
git rebase -i HEAD~3
```

把目标提交改成：

```text
edit a1 docs: add day 24 outline
pick b2 docs: add examples
pick c3 docs: add exercises
```

Git 会停在 `a1` 这个提交。

然后你可以修改文件，再执行：

```bash
git add <file>
git commit --amend --no-edit
git rebase --continue
```

意思是：修改这个历史提交，然后继续把后面的提交重新应用回来。

## 场景七：拆分一个太大的提交

有时候一个提交里混了很多事情，例如：

```text
a1 docs: update git notes
```

但它里面同时改了：

- Day 23 rebase
- Day 24 整理提交
- README 链接

这种提交 review 起来很难，可以拆成多个提交。

步骤：

```bash
git rebase -i HEAD~3
```

把那个太大的提交改成 `edit`：

```text
edit a1 docs: update git notes
pick b2 docs: add examples
pick c3 docs: add exercises
```

Git 停下来后，先把这个提交拆回工作区：

```bash
git reset HEAD^
```

然后分批暂存并提交：

```bash
git add docs/days/day23.md
git commit -m "docs: deepen rebase guide"

git add docs/days/day24.md
git commit -m "docs: add commit cleanup practice"

git add README.md
git commit -m "docs: link new daily notes"
```

最后继续 rebase：

```bash
git rebase --continue
```

如果只想挑选文件里的部分改动，可以用：

```bash
git add -p
```

`git add -p` 会一段一段问你要不要暂存，适合拆分混在同一个文件里的改动。

## 整理失败怎么办

如果 rebase 过程中发现不对，优先用：

```bash
git rebase --abort
```

如果 rebase 已经结束，但你发现整理错了，可以看：

```bash
git reflog
```

找到整理前的 commit id，再回去：

```bash
git reset --hard <old-commit-id>
```

这也是为什么整理前建备份分支很有用。

## 推送前注意

整理提交历史会改写 commit id。

如果这些提交还没推送，正常推送即可：

```bash
git push origin main
```

如果这是你自己的功能分支，并且你已经推送过，整理后可能需要：

```bash
git push --force-with-lease origin feature/demo
```

不要随便对多人共享的 `main` 使用强制推送。

## 你应该看到

`git rebase -i HEAD~3` 打开后是这样一份待办清单：

```text
pick a1b2c3d docs: add day 24 outline
pick b2c3d4e fix typo
pick c3d4e5f add missing example
```

把后两行改成 `fixup` 保存，三次提交合并成一次，观察 `git log --oneline`：

```text
$ git log --oneline -3
7d4e2f1 docs: add day 24 outline
9c1b8a0 docs: deepen rebase guide
4f6a2c3 init docs
```

原来的三个 commit id 全都不见了，说明历史确实被重写。如果结果不满意，可以用 `git reflog` 或整理前建的 `backup/before-cleanup` 分支回去。

## 今日练习

1. 创建一个练习分支：

```bash
git switch -c feature/cleanup-demo
```

2. 连续做 3 个小提交：

```text
docs: add cleanup outline
fix typo
add missing example
```

3. 执行：

```bash
git rebase -i HEAD~3
```

4. 用 `fixup` 把后两个提交合并到第一个提交。
5. 再做一个提交信息很差的提交，例如 `update`。
6. 用 `git commit --amend` 改成清晰的提交信息。
7. 用下面命令观察整理后的历史：

```bash
git log --oneline --graph --decorate -5
```

## 检查点

你应该知道：

- `git commit --amend` 可以修改最近一次提交
- `git rebase -i` 可以整理多个历史提交
- `reword` 用来改提交信息
- `squash` 和 `fixup` 用来合并提交
- `drop` 会删除提交
- `edit` 可以修改历史提交内容
- `git add -p` 可以帮助拆分提交
- 整理提交历史前，先确认这些提交没有影响别人
