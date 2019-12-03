# Mac 使用ssh自动登录服务器

通常情况，我们使用ssh链接到服务器，但是，如果因为某些原因，需要频繁登录不同到ssh到时候，不断到去复制host地址和密码是一个非常无价值到行为，本文的目的就是配置成一个可执行到快捷指令，在想登录特定服务器时候，只需要 `sh 165` 就可以自动登录到xxx.xxx.xxx.165的机器上。

## 用到到文件

> autoSSH.sh

该文件的目的是读取ssh链接所需要到参数，例如host，user等

> ssh_auto_login.exp

expect用来完成跟terminal的交互，用户输入密码的行为

> ssh_pwd.json

用来存储需要用到到ssh所有信息

> .bash_profile / .zshrc

用来绑定快捷键
