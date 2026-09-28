# Day 15：克隆仓库

## 学习目标

从远程复制一个完整项目到本地。

## 核心概念

`clone` 会下载仓库文件、提交历史，并自动配置远程地址。

## 常用命令

```bash
git clone https://github.com/your-name/your-repo.git
git remote -v
```

## 你应该看到

克隆时 Git 会下载对象并解包，进度走完后本地就有一个同名目录：

```text
$ git clone https://github.com/your-name/your-repo.git
Cloning into 'your-repo'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 12 (delta 2), reused 12 (delta 2), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (2/2), done.
```

进入目录后检查远程地址，`origin` 会自动指向克隆来源：

```text
$ cd your-repo
$ git remote -v
origin  https://github.com/your-name/your-repo.git (fetch)
origin  https://github.com/your-name/your-repo.git (push)
```

`git log --oneline` 能看到原仓库里已有的提交，说明克隆不只拿到文件，还拿到了完整历史。

## 今日练习

1. 新建一个空目录。
2. 克隆自己的练习仓库。
3. 进入仓库后执行 `git remote -v`。
4. 执行 `git log --oneline` 查看历史。

## 检查点

你应该知道：克隆得到的不只是文件，还有完整的 Git 历史。

