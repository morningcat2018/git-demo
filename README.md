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

# 目录

- [1-基础命令](1-基础命令.md)
- [2-日志](2-日志.md)
- [3-分支与合并](3-分支与合并.md)
- [4-远程仓库协作](4-远程仓库协作.md)
- [5-版本回溯](5-版本回溯.md)
- [6-开发流程](6-开发流程.md)
- [7-gitstash](7-gitstash.md)
- [8-other](8-other.md)