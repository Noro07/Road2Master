# shell 脚本间的值传递

example:
【a.sh】
SET_VALUE="TEST"
echo $SET_VALUE
echo SET_VALUE=$SET_VALUE >> .stage_docker

【b.sh】
source .stage_docker
echo \${SET_VALUE}
