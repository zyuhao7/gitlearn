# Day 04：第一次提交

## 学习目标

完成第一次 `commit`，理解提交就是保存一个版本快照。

## 核心概念

提交会把暂存区中的内容保存到本地仓库。每次提交都应该描述这次改动做了什么。

## 常用命令

```bash
git add README.md
git commit -m "add readme"
```

## 提交信息建议

好的提交信息：

```text
add readme
fix typo in readme
docs: add git notes
```

不推荐：

```text
update
test
111
```

## 你应该看到

提交成功后，Git 会打印分支名、提交编号、提交信息和本次改动行数：

```text
$ git add README.md
$ git commit -m "add readme"
[main (root-commit) 1a2b3c4] add readme
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

`1a2b3c4` 是这次提交的编号前缀，每次提交都不一样。第一次提交会带 `root-commit` 字样，表示这是仓库的第一个提交。较老版本的 Git 或老仓库里，方括号中可能显示 `master` 而不是 `main`，那是默认分支名的差异，不影响提交本身。

## 常见报错

- `*** Please tell me who you are.`：还没配置提交身份。先执行一次：

  ```bash
  git config --global user.name "你的名字"
  git config --global user.email "你的邮箱"
  ```

  配置好之后再执行原来的 `git commit`，这次提交并没有成功，不需要重复 `git add`。
- `nothing added to commit but untracked files present`：暂存区是空的，改动还没 `git add`。先暂存再提交。
- `nothing to commit, working tree clean`：工作区和暂存区都没有改动，没有东西可提交。确认文件是不是真的保存了。

## 今日练习

1. 暂存 `README.md`。
2. 提交一次。
3. 提交信息写清楚做了什么。

## 检查点

你应该知道：只有 `git commit` 后，改动才真正进入版本历史。

