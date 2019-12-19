# Mac 使用 ssh 自动登录服务器

通常情况，我们使用 ssh 链接到服务器，但是，如果因为某些原因，需要频繁登录不同到 ssh 到时候，不断到去复制 host 地址和密码是一个非常无价值到行为，本文的目的就是配置成一个可执行到快捷指令，在想登录特定服务器时候，只需要 `sh 110` 就可以自动登录到 xxx.xxx.xxx.110 的机器上。

## 用到到文件

> autoSSH.sh

该文件的目的是读取 ssh 链接所需要到参数，例如 host，user 等

> ssh_auto_login.exp

expect 用来完成跟 terminal 的交互，用户输入密码的行为

> ssh_pwd.json

用来存储需要用到到 ssh 所有信息

> .bash_profile / .zshrc

用来绑定快捷键

## autoSSH.sh

```bash
#!/bin/bash
JQ_EXEC=`which jq`
FILE_PATH=~/ssh_pwd.json

sshJson () {
 serverHost=$(cat $FILE_PATH | ${JQ_EXEC} .$1.host | sed 's/\"//g')
 serverUser=$(cat $FILE_PATH | ${JQ_EXEC} .$1.user | sed 's/\"//g')
 serverPwd=$(cat $FILE_PATH | ${JQ_EXEC} .$1.pwd | sed 's/\"//g')
}

case $1 in
 110)
  sshJson aTestServer
  ;;
 *)
  echo "no match"
  ;;
esac

expect -f ~/ssh_auto_login.exp $serverHost $serverUser $serverPwd
```

### jq

这里使用 jq 用来读取 json 数据。因为不同安装环境的 jq 可能所在位置不同，所以这里用 which jq 的返回值来动态获取。`.$1.host`这里的`.`是对应的 json 里面的 key。不建议用数字来作为 key，会出现异常，当然如果是数组的话使用`["1"]`

### expect

这里使用 expect 来调用 exp 脚本，三个参数对应 host，user，pwd

## ssh_auto_login.exp

```expect
#!/usr/bin/expect -f

set TARGET [lindex $argv 0]
set USER [lindex $argv 1]
set PWD [lindex $argv 2]
set LOG [lindex $argv 3]
set timeout 30

spawn ssh $USER@$TARGET
expect {
    "*yes/no" {send "yes\r"; exp_continue}
    "*password:" {send "$PWD\r"}
}

if {"logs" eq $LOG} {
 expect {
  "#" {send "tail -f ~/.pm2/logs/npm-out.log\r"}
 }
}

interact
```

`expect` 用来监听返回值，例如上面出现的`"*yes/no"`，将会监听返回值是否包含 yes/no，如果有，则执行`{}`中的数据
`send` 用来输入值
`interact` 用户进入交互阶段

expect 如果没有需要安装，可以使用 brew 来安装，which expect 查到对应的位置放在.exp 文件的第一行

## ssh_pwd.json

用来记录 ssh 相关信息

```json
{
  "aTestServer": {
    "host": "xxx.xxx.xxx.110",
    "user": "username",
    "pwd": "pwd",
    "desc": "This is a test"
  }
}
```

## .bash_profile / .zshrc

alias sh='sh ~/autoSSH.sh'

编辑完后记得 source 一下

---

到此为止，就可以使用 `sh 110` 来自动链接到对应的 server

---

ref:
<https://blog.csdn.net/qq_34908844/article/details/88402199>
