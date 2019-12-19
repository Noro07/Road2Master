# Git commit 修改用户名和邮箱

在有些特殊情况下，我们可能会使用不合适的用户名或者邮箱提交了commit的记录，而因为已经push上去了所以可以使用的方法有限，这里提供一个方法，可以修改所有的记录，但是相对危险，而且不推荐在公共的git上使用

## 配置当前项目的用户名和邮箱

默认情况，git在没有local config中找到用户名和邮箱的时候，会使用global config里面的设置。所以这里我先修改成当前我们想要的那个用户名和邮箱

```bash
git config user.name 'Noro07'
git config user.email 'uniform328@gmail.com'
```

## 创建修改用户名和邮箱的脚本

在项目的根目录下创建一个`shell`脚本，名字随意。这里我使用email.sh,修改下面出现的`OLD_EMAIL`, `CORRECT_NAME`和`CORRECT_EMAIL`

```bash
#!/bin/sh

git filter-branch --env-filter '

OLD_EMAIL="oldEmail"
CORRECT_NAME="newName"
CORRECT_EMAIL="newEmail"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

## 运行脚本

执行刚才编辑的shell脚本，这里macOS使用下列指令

> sh ./email.sh

## 推到远程

覆盖origin的commit记录，至此结束

> git push origin --force --all

## 第二次执行报错怎么办

当修改完第一遍发现改错了，还想改，如是试图再次执行这个shell脚本，很遗憾，遇到了一个错误

```bash
Cannot create a new backup.
A previous backup already exists in refs/original/
Force overwriting the backup with -f
```

这里是因为之前执行的时候，已经创建了一个备份，所以需要覆盖掉之前的备份。这里注意，如果要强制覆盖，会导致之前的备份丢失，如果是公共项目，请谨慎。
执行以下语句清除，之后就可以按照上述方法在执行一次了。

> git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch Rakefile' HEAD

Ref:<https://cloud.tencent.com/developer/article/1352623>
