# 初始化并推送到github

```bash
echo "# git-demo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:morningcat2018/git-demo.git
git push -u origin main
```

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

- git add `<file>`
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

# git restore

- git restore `<file>`
- 撤销	
- 丢弃工作区中文件的修改（Git 2.23+ 推荐）。
- git restore --staged `<file>`
- 撤销	
- 将文件从暂存区移回工作区（撤销 git add）。

```bash
➜  git-demo git:(main) ✗ touch file1.txt
➜  git-demo git:(main) ✗ echo "git" >> file1.txt 
➜  git-demo git:(main) ✗ git add .
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

➜  git-demo git:(main) ✗ git restore --staged file1.txt 
➜  git-demo git:(main) ✗ git status                    
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file1.txt

➜  git-demo git:(main) ✗ cat file1.txt 
git
➜  git-demo git:(main) ✗ 
```
由此可见 git restore --staged `<file>` 是将文件从暂存区移回工作区, 即撤销git add 的效果

```bash
➜  git-demo git:(main) ✗ echo "hello" >> file1.txt 
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

➜  git-demo git:(main) ✗ cat file1.txt 
git
hello
➜  git-demo git:(main) ✗ git restore file1.txt 
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

➜  git-demo git:(main) ✗ cat file1.txt 
git
➜  git-demo git:(main) ✗ 
```

丢弃工作区中文件的修改, 是将还没有git add的文件里的修改撤销会git add之前的状态

```bash
➜  git-demo git:(main) ✗ echo "hello" >> file1.txt 
➜  git-demo git:(main) ✗ cat file1.txt 
git
hello
➜  git-demo git:(main) ✗ git add file1.txt 
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

➜  git-demo git:(main) ✗ echo "hello2" >> file1.txt
➜  git-demo git:(main) ✗ cat file1.txt 
git
hello
hello2
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

➜  git-demo git:(main) ✗ git restore file1.txt 
➜  git-demo git:(main) ✗ cat file1.txt 
git
hello
➜  git-demo git:(main) ✗ git status           
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
	new file:   file1.txt

➜  git-demo git:(main) ✗ 
```

# git log

- git log
- git log -n 3
    - 查看最近N条的提交日志
- git log --oneline --graph
    - 查看
    - 以图形化方式简洁查看提交历史分支走向

```bash
➜  git-demo git:(main) ✗ git log --oneline --graph
* 03582f7 (HEAD -> main) git restore
* 924a65c git commit -a 可以不git add 直接提交
* 927c329 关于git add 和 git commit 的用法 以及git commit --amend
* baa0a1b (origin/main) first commit
```

commit 924a65c 不是一个正确提交,若想要修改可以使用 git rebase

```
➜  git-demo git:(main) git rebase -i 924a65c^
pick 924a65c # git commit -a 可以不git add 直接提交
pick 03582f7 # git restore

# Rebase 927c329..03582f7 onto 927c329 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~   

改为

reword 924a65c # git commit -a 可以不git add 直接提交

重新输入信息:git comit 作废

956477c (HEAD -> main) git restore
a264a0e git comit 作废
927c329 关于git add 和 git commit 的用法 以及git commit --amend
baa0a1b (origin/main) first commit
```

# 查看修改内容

1. git diff

- git diff `<file>`
    - 看某个文件的修改内容
- git diff --staged `<file>`
- git diff --cached `<file>`
    - git diff --staged 和 git diff --cached 效果相同
    - 用来查看“即将提交的内容”, 即查看已经 git add 之后的改动
- git diff commit1 commit2
    - 看历史版本之间的差异
    - git diff HEAD~1 HEAD 看“上一个版本 vs 当前版本”
- 小技巧
    - git diff --color 更容易阅读
    - git diff | less 分页阅读

```
➜  git-demo git:(main) echo "file2" >> file2.txt
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

刚创建的新文件使用 git diff file2.txt 查看不到修改内容

git add 之前使用 git diff `<file>`, 对比的是与git add 之前的不同项
```
➜  git-demo git:(main) ✗ git add .
➜  git-demo git:(main) ✗ git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   file2.txt



➜  git-demo git:(main) ✗  echo "..." >> file2.txt
➜  git-demo git:(main) ✗ git diff file2.txt 

diff --git a/file2.txt b/file2.txt
index 6c493ff..6d520ab 100644
--- a/file2.txt
+++ b/file2.txt
@@ -1 +1,2 @@
 file2
+...
```

git add 之后使用 git diff --staged `<file>`, 对比的是与git commit 之前的不同项
```
➜  git-demo git:(main) ✗ git add .
➜  git-demo git:(main) ✗ git diff --staged file2.txt 

diff --git a/file2.txt b/file2.txt
new file mode 100644
index 0000000..6d520ab
--- /dev/null
+++ b/file2.txt
@@ -0,0 +1,2 @@
+file2
+...

➜  git-demo git:(main) ✗ git diff --cached file2.txt 
```

2. git show `<commit-id>`

看某个 commit 修改了什么

```
➜  git-demo git:(main) ✗ git log --oneline
➜  git-demo git:(main) ✗ git show 956477c
➜  git-demo git:(main) ✗ 
```

只看某个文件在那个 commit 的变化

> git show 956477c -- file2.txt


