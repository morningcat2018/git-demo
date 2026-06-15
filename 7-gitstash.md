1. git stash

git stash 是 Git 里专门用来**临时“收起当前修改”**的工具，非常适合“代码写一半但要切分支”的场景。

git stash = 把当前未提交的修改先存起来，让工作区变干净，之后再恢复

```
你正在开发：

main.py（改了一半）

突然要：

.切分支修 bug
.pull 最新代码
.临时处理紧急任务

但 Git 不让你切：

error: Your local changes would be overwritten

👉 这时候就用：

git stash



执行：git stash

Git 会：

保存当前修改（包括 staged + unstaged）
恢复工作区到“干净状态”

📦 状态变化
之前：
working tree:  A + 修改中
stash 后：
working tree:  A（干净）
stash:         保存了你的修改
```

带备注

git stash save "fix login bug"

or

git stash push -m "fix login bug"


2. git stash list

查看 stash 列表

3. git stash apply

恢复最近一次 stash

恢复但不删除 stash

---

git stash apply stash@{2}

应用指定 stash

git stash drop stash@{0}

删除 stash

4. git stash pop

恢复并删除 stash（最常用）

5. git stash show

查看内容

git stash show -p

查看详细内容