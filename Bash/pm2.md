# 进程守护

> pm2 start npm -- start --watch

启动参数说明：

- --watch：监听应用目录的变化，一旦发生变化，自动重启。如果要精确监听、不见听的目录，最好通过配置文件。
- -i --instances：启用多少个实例，可用于负载均衡。如果-i 0 或者-i max，则根据当前机器核数确定实例数目。
- --ignore-watch：排除监听的目录/文件，可以是特定的文件名，也可以是正则。比如--ignore-watch="test node_modules "some scripts""
- -n --name：应用的名称。查看应用信息的时候可以用到。
- -o --output \<path>：标准输出日志文件的路径。
- -e --error \<path>：错误输出日志文件的路径。
- --interpreter \<interpreter>：the interpreter pm2 should use for executing app (bash, python...)。比如你用的 coffee script 来编写应用。

pm2 log默认地址 `$HOME/.pm2/logs/XXX-err.log` XXX是app的名字

---

ref:
<https://www.cnblogs.com/fyc119/p/6959593.html>
