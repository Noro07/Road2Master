# MAC network link conditioner

## 问题

安装后因为某些原因在系统偏好设置中找不到，选择打开 additional tool 中是 hardware 中的 network link conditioner 会提示 preferences is installed with macos and can’t be replaced

## 解决方案

直接在/Library/PreferencePanes 下复制 network link conditioner 就可以在系统设置中重现这个图标

疑问

1. 如果现在 remove 这个设置，原有设置是否会保留
2. 再次安装，是按照在 additional tool 中直接打开，还是选择上述方法再次操作
