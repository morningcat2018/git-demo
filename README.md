# 初始化并推送到github

echo "# git-demo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:morningcat2018/git-demo.git
git push -u origin main

# git status

查看工作区和暂存区的文件状态

```bash
➜  git-demo git:(main) git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

# git add 

- git add <file>	
    - 暂存	
    - 将指定文件添加到暂存区。
- git add .	
    - 暂存	
    - 添加当前目录下的所有变更（新增、修改、删除）。

```bash
➜  git-demo git:(main) ✗ git add README.md 
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md

```
# git commit

- git commit -m "message"
    - 提交	
    - 将暂存区的文件提交到本地仓库，并附上提交信息。
- git commit --amend
    - 提交	
    - 修改最近一次提交的信息或补充遗漏的文件

```bash
➜  git-demo git:(main) ✗ git commit -m "关于git add 和 git commit 的用法"
[main d72104f] 关于git add 和 git commit 的用法
 1 file changed, 59 insertions(+), 1 deletion(-)

➜  git-demo git:(main) ✗ git log -n 3
 commit d72104f9cc19fe17cebe79f0b20faf3d238c61b2 (HEAD -> main)
Author: morningcat <morningcat2018@qq.com>
Date:   Mon Jun 15 23:32:07 2026 +0800

    关于git add 和 git commit 的用法

commit baa0a1b26893041136980456f32ec50b1b5a99da (origin/main)
Author: morningcat <morningcat2018@qq.com>
Date:   Mon Jun 15 23:19:34 2026 +0800

    first commit

➜  git-demo git:(main) ✗ git commit --amend
[main 927c329] 关于git add 和 git commit 的用法 以及git commit --amend
 Date: Mon Jun 15 23:32:07 2026 +0800
 1 file changed, 59 insertions(+), 1 deletion(-)

➜  git-demo git:(main) ✗ git log -n 3
commit 927c3293b608c28e87c3537d3cb375555d5a960a (HEAD -> main)
Author: morningcat <morningcat2018@qq.com>
Date:   Mon Jun 15 23:32:07 2026 +0800

    关于git add 和 git commit 的用法
    以及git commit --amend

commit baa0a1b26893041136980456f32ec50b1b5a99da (origin/main)
Author: morningcat <morningcat2018@qq.com>
Date:   Mon Jun 15 23:19:34 2026 +0800

    first commit
```

# 可以不git add直接git commit

```bash


```