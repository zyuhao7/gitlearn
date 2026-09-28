# Day 30：综合实战

## 学习目标

完成一次接近真实项目的 Git 协作流程。

## 实战任务

1. 更新主分支。
2. 创建功能分支。
3. 新增学习总结文件。
4. 提交修改。
5. 推送分支。
6. 创建 Pull Request。
7. 合并回主分支。

## 参考命令

```bash
git switch main
git pull
git switch -c feature/final-practice
mkdir -p notes
echo "# Final Practice" > notes/final-practice.md
git add notes/final-practice.md
git commit -m "docs: add final practice notes"
git push -u origin feature/final-practice
```

## 你应该看到

推送新分支时，远端会提示这是一个新分支，并帮你建立跟踪关系：

```text
$ git push -u origin feature/final-practice
To github.com:user/my-git-practice.git
 * [new branch]      feature/final-practice -> feature/final-practice
branch 'feature/final-practice' set up to track 'origin/feature/final-practice'.
```

在网页上创建 Pull Request 并合并回 `main` 之后，本地切回 main 再拉取，就能看到合并结果：

```bash
git switch main
git pull
```

`git log --oneline` 里能看到你自己的提交已经进入 `main`，30 天练习到此闭环。

## 总结清单

完成 30 天后，你应该掌握：

- 初始化仓库
- 添加和提交文件
- 查看历史和差异
- 使用分支
- 合并和解决冲突
- 连接远程仓库
- 推送和拉取代码
- 撤销错误修改
- 使用 tag、stash、rebase、cherry-pick
- 理解 Pull Request 协作流程

## 检查点

你应该能独立完成一次从创建分支到提交 PR 的完整流程。

