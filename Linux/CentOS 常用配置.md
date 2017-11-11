# CentOS 常用配置

## 配置 PATH 环境变量

* 可以修改用户目录下的 .bash_profile 文件来配置 PATH 环境变量
* 大概在倒数第 3 行，有一行 PATH=$PATH:$HOME/bin，将其修改为 PATH=$PATH:$HOME/bin:[Node.js路径]
* 断开并重新连接服务器，使PATH环境变量生效
* 在用户目录输入 node -v，显示版本号，说明配置成功