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

```