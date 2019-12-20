# Git

## git 放弃当前没有 commit 的代码改动

> git checkout .

## This will unstage all files you might have staged with git add

> git reset

## 回滚到上个 commit

> git reset --hard HEAD~1

## 要合并从 HEAD 版本开始往过去数 3 个版本

> git rebase -i HEAD~3

## 删除远程分支

> git push origin --delete Su-modify

## 删除本地分支

> git branch -d Su-modify

## 强行删除本地分支

> git branch -D Su-modify

## Configuring a remote for a fork

给 fork 配置一个 remote
使用 git remote -v 查看远程状态

```bash
git remote -v
# origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
# origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
```

添加一个将被同步给 fork 远程的上游仓库

> git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

查看状态确认是否配置成功

```bash
git remote -v
# origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
# origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
# upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
# upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

## Syncing a fork

- 从上游仓库 fetch 分支和提交点，传送到本地，并会被存储在一个本地分支 upstream/master

> git fetch upstream

```bash
git fetch upstream
# remote: Counting objects: 75, done.
# remote: Compressing objects: 100% (53/53), done.
# remote: Total 62 (delta 27), reused 44 (delta 9)
# Unpacking objects: 100% (62/62), done.
# From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
#  * [new branch]      master     -> upstream/master
```

- 切换到本地主分支(如果不在的话)

> git checkout master

```bash
git checkout master
# Switched to branch 'master'
```

- 把 upstream/master 分支合并到本地 master 上，这样就完成了同步，并且不会丢掉本地修改的内容

> git merge upstream/master

```bash
git merge upstream/master
# Updating a422352..5fdff0f
# Fast-forward
#  README                    |    9 -------
#  README.md                 |    7 ++++++
#  2 files changed, 7 insertions(+), 9 deletions(-)
#  delete mode 100644 README
#  create mode 100644 README.md
```

- 如果想更新到 GitHub 的 fork 上，直接 git push origin master 就好了

## ???

```bash
 git fetch upstream
 git checkout -b copyright upstream/master
```

先克隆 在设置上游 再同步
