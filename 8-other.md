
# git cherry-pick `<commit>`

git cherry-pick `<commit>` 是 Git 里一个非常“精确搬运代码”的命令，可以把某个提交从一个分支单独拿过来应用到当前分支。

git cherry-pick = 把某个 commit “复制”到当前分支（生成一个新的 commit）

```
假设有两个分支：

main:    A --- B --- C
                 \
feature:          D --- E

你在 feature 分支写了一个很好的 commit：

E: add login validation

但你不想 merge 整个 feature，只想要 E：

执行：

git switch main
git cherry-pick E

👉 结果：

main:    A --- B --- C --- E'
                 \
feature:          D --- E

注意：

E' 是新 commit
内容和 E 一样，但 hash 不同


常用用法
📌 1）cherry-pick 单个 commit
git cherry-pick <commit-hash>

📌 2）多个 commit
git cherry-pick A B C

或范围：
git cherry-pick A^..C

📌 3）如果冲突
CONFLICT

解决后：

git add .
git cherry-pick --continue

📌 4）放弃 cherry-pick
git cherry-pick --abort
```

# git rebase `<branch>`

把当前分支“挪到”另一个基底上，并重新应用提交历史

把你的提交“搬家”，让历史变成一条更直的线

```
假设你在开发 feature 分支：

main:    A --- B --- C
                 \
feature:          D --- E

此时 main 更新了：

main:    A --- B --- C --- F --- G


如果你 rebase：
git switch feature
git rebase main

结果变成：
main:    A --- B --- C --- F --- G
                                 \
feature:                          D' --- E'

注意：
D、E 被“重新复制”为 D'、E'
feature 的起点变成最新 main

把当前分支的 commit “摘下来”，再一个个“重新放到”目标分支后面



📌 merge：
A---B---C---M
        \   /
         D-E

📌 rebase：
A---B---C---F---G---D'---E'
```

```
常见用法
📌 1）把当前分支基于 main 更新
git rebase main
📌 2）交互式 rebase（最强功能）
git rebase -i HEAD~3

👉 可以：

修改 commit message
合并 commit（squash）
删除 commit
调整顺序

示例：
pick A
pick B
pick C

改成：

pick A
squash B
squash C

👉 合并成一个 commit

📌 3）解决冲突
CONFLICT

处理后：

git add .
git rebase --continue
📌 4）放弃 rebase
git rebase --abort
```

```
非常重要的原则（面试必问）

不要在已经 push 的公共分支上 rebase

因为：

commit hash 会变
其他人历史会乱

---

❌ 错误用法：
git push
git rebase
git push --force

👉 会污染团队历史



使用建议
👍 推荐：
本地开发分支
feature 分支整理历史
合并前整理 commit

👎 不推荐：
shared/main/master 分支
团队已经同步的分支
```

# git worktree

让一个 Git 仓库同时拥有多个工作目录（多个分支并行开发）

一个仓库，多份代码目录，各自切不同分支同时开发

git worktree 让你可以同时在多个分支上开发，不需要 stash、不需要频繁切换目录，是 Git 的“多线程开发模式”。

```
基本用法
📌 1）添加一个新的 worktree
git worktree add ../feature-x feature-x

含义：

在 ../feature-x 创建新目录
检出 feature-x 分支

📌 2）创建新分支 + worktree
git worktree add -b new-feature ../new-feature main

👉 含义：

基于 main 创建 new-feature 分支
在新目录中打开

📌 3）查看所有 worktree
git worktree list

输出类似：

/path/repo        abc123 [main]
/path/feature-x   def456 [feature-x]

📌 4）删除 worktree
git worktree remove ../feature-x



工作原理（核心理解）

普通 Git：

.git = 所有历史 + 对象库
working dir = 当前分支

worktree：

一个 .git
多个 working directory
共享同一个 object database

本质：多个“工作区”，共享一个 Git 数据库



注意事项
❗ 1）不能两个 worktree 同时用同一个分支
feature-x 只能在一个目录里 checkout

否则报错：

already checked out
```

# git reflog

