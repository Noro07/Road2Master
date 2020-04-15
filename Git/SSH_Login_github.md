# 配置GitHub账户的SSH

## 生成公钥和私钥

1. 打开**git bash**
2. `cd ~/.ssh` 查看是否已经生成过SSH
3. `ssh-keygen -t rsa -C "邮箱"` 三次回车（为什么按三下，是因为有提示你是否需要设置密码，如果设置了每次使用Git都会用到密码，一般都是直接不写为空，直接回车就好了）会在一个文件夹里面生成一个私钥 id_rsa和一个公钥id_rsa.pub
4. 执行查看公钥的命令`cat ~/.ssh/id_rsa.pub `

## GitHub 存储公钥

1. 打开GitHub账户
2. 选择**settings**
3. 点击**SSH and GPG keys**
4. 点击**new key**
5. 输入一个Title名字，然后复制**id_rsa.pub**，把文件内容复制到key的输入框中，保存
