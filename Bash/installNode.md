# 在指定目录下安装 node

有时候出于某些原因，我们需要将 node 安装在特定的目录下，而非自动安装的目录

ref: <https://www.cnblogs.com/fps2tao/p/9956139.html>

下载

//下载(没有 wget,运行 yum install wget -y)
wget https://nodejs.org/dist/v9.8.0/node-v9.8.0-linux-x64.tar.xz
//解压
xz -d node-v9.8.0-linux-x64.tar.xz
tar -xvf node-v9.8.0-linux-x64.tar

cd node-v\*

将 bin 文件添加到 PATH

## 修改方法二

通过修改.bashrc 文件:
vim ~/.bashrc
//在最后一行添上：
export PATH=/usr/local/mongodb/bin:\$PATH
生效方法：（有以下两种）
1、关闭当前终端窗口，重新打开一个新终端窗口就能生效
2、输入“source ~/.bashrc”命令，立即生效 有效期限：永久有效 用户局限：仅对当前用户

又例如
<https://www.jianshu.com/p/766b96184eb1>

## {install_path} 安装目录路径

1. 安装 wget
   yum install wget

2. 下载对应文件
   wget -c https://nodejs.org/dist/v8.9.1/node-v8.9.1-linux-x64.tar.xz

3. 解压
   tar -xvf node-v8.9.1-linux-x64.tar.xz

4. 重命名
   mv node-v8.9.1-linux-x64 nodejs

5. 创建连接 放在 /usr/local/bin 文件夹下
   pwd 查看路径
   sudo ln -s {install_path}/nodejs/bin/node /usr/local/bin/node
   sudo ln -s {install_path}/nodejs/bin/npm /usr/local/bin/npm

6. 查看版本
   node --version

7. 解决 npm 安装失效问题
   sudo vim /etc/profile

   在文件的底部，添加下面两行代码：
   export NODE_HOME={install_path}/nodejs/bin
   export PATH=$NODE_HOME:$PATH

8. 更新 profile 更改
   source /etc/profile

9. 安装 cnpm （很多时候用 npm 安装其他的插件会失败，用 cnpm，当然也有相反情况）
   npm install -g cnpm --registry=https://registry.npm.taobao.org
