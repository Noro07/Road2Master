# 本地和服务器的文件复制

## 上传本地文件到服务器

> scp /path/filename username@servername:/path/

## 复制服务器文件到本地

> scp -r user@your.server.example.com:/path/to/foo /Users/ziyi/Documents

`-r` 指文件夹

## 文件打包

打包： tar -zcvf  目标文件 源文件或文件夹
目标文件为要打包成的文件的文件名， 打包后文件的 格式取决于目标文件的后缀名
单文件或文件夹打包

> tar -zcvf index.tar.gz index.html

此时的结果是将 index.html 打包为 tar 并压缩为 gz 了，如果后缀名不加 .gz 则不压缩，金打包
多文件或文件夹 混合打包

> tar -zcvf index.tar.gz index.html css/ js/ images/

此时则将多个文件及文件夹打包到一个包里并压缩，index.html css/ js/ images/ 打包并压缩为 index.tar.gz
