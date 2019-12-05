# nvm 在 terminal 第一次加载卡顿

terminal 在初始化的时候会卡顿一下，导致在 `cmd` + `n` 打开新窗口的时候，都会有卡顿，这个是无法避免的。除非改用 n 来管理 node 版本，当然如果能接受 n，这是最好的解决方案，不然的话，选择 nvm 延迟触发的方法。当用户输入 nvm 时候，才加载 nvm 模块。当然用户可能会直接输入 node 或者 npm，所以这里将这两个关键字也包含其中。将以下代码加入 `.bash_profile`或者 `.zshrc`

```bash

[ ! -r ~/.nvm/nvm.sh ] || {
 function nvm() {
  unset -f nvm node npm
  . ~/.nvm/nvm.sh
  nvm use node >/dev/null
  [ ! -r ~/.nvm/bash_completion ] || . ~/.nvm/bash_completion
  nvm ${1+"$@"}
 }

 function node() {
  nvm --version >/dev/null 2>&1
  node ${1+"$@"}
 }

 function npm() {
  nvm --version >/dev/null 2>&1
  npm ${1+"$@"}
 }
}

```
