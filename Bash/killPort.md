# 端口占用

sudo lsof -i :3000

COMMAND   PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    61342 a  313u  IPv6 0x1111111111111     0t0  TCP \*:cslistener (LISTEN)

然后根据 PID 杀进程：
sudo kill -9 61342
