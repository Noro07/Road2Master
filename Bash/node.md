# node

## 使用 n 升级 node.js

npm 中有一个模块叫做“n”，专门用来管理 node.js 版本的。
更新到最新的稳定版只需要在命令行中打下如下代码：

> npm install -g n
> n stable

如需最新版本则用 n latest
￼
当然，n 后面也可以跟具体的版本号：n v6.2.0
node.js 升级就是这么简单。
升级 npm
npm 升级就更简单了，只需要在终端中输入：

> npm -g install npm@next

## npm 安装中显示细节

> npm install --loglevel silly
