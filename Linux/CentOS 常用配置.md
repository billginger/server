# CentOS 常用配置

## 更改 SSH 默认端口

编辑配置文件 `vi /etc/ssh/sshd_config`，找到 `#Port 22`，去掉注释，改为新的端口号，保存后退出。

CentOS6 执行重启命令 `/etc/init.d/sshd restart`。

CentOS7 执行重启命令 `systemctl restart sshd.service`。

断开连接重新连接，如连接不上，请检查是否已在“安全组”开启新的端口。

## 配置 PATH 环境变量

* 可以修改用户目录下的 .bash_profile 文件来配置 PATH 环境变量
* 大概在倒数第 3 行，有一行 PATH=$PATH:$HOME/bin，将其修改为 PATH=$PATH:$HOME/bin:[Node.js路径]
* 断开并重新连接服务器，使PATH环境变量生效
* 也可以使用 source .bash_profile 命令使环境变量生效
* 在用户目录输入 node -v，显示版本号，说明配置成功

## 查看与设定别名

使用 `alias` 命令查看系统中所有的命令别名

暂时设定别名：
`alias 别名='原命令'`

暂时删除别名：
`unalias 别名`

要使别名永久生效，可以修改用户目录下的 .bashrc 文件，追加以下内容：

```s
alias 别名='原命令'
```

## 自定义命令行提示符

可以修改用户目录下的 .bashrc 文件，追加以下内容：

```s
# Custom command line prompt
export PS1='\[\e[32;1m\][\w]\$\[\e[m\] '
```

不要写成下面这样（命令比较长时会错位）：

```s
export PS1='\e[32;1m[\w]\$\e[m '
```

带上时间：

```s
export PS1='\[\e[32;1m\][\t \w]\$\[\e[m\] '
```

* $PS1 默认值为 '[\u@\h \W]\$ '
* \u 表示当前用户名，\h 表示短主机名，\W 表示短路径，\$ 表示提示符
* \[\e[32;1m\] 用来设置字体颜色，32 代表绿色，1 代表高亮显示
* \w 表示长路径
* \[\e[m\] 用来关闭颜色设置，否则提示符后面输入的命令也会变成彩色的
* \t 表示24小时制的时间 HH:MM:SS
