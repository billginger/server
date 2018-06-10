# 在 CentOS 下配置 Node.js 运行环境

## 安装 Git

```
yum install git
```

## 生成 Git SSH 密钥

```
ssh-keygen -t rsa -C "BaiduYun"
cat ~/.ssh/id_rsa.pub
```

复制 .pub 文件的内容到 GitHub 的 SSH keys 中。

## 从 GitHub 克隆代码

```
git clone git@github.com:billginger/wechat.git wechat
```

## 安装 Node.js

### 下载

```
wget https://nodejs.org/dist/v8.11.2/node-v8.11.2-linux-x64.tar.xz
```

### 解压

```
tar xf node-v8.11.2-linux-x64.tar.xz
```

### 重命名目录

```
mv node-v8.11.2-linux-x64 node
```

### 配置 PATH 环境变量

* 可以修改用户目录下的 .bash_profile 文件来配置 PATH 环境变量
* 大概在倒数第 3 行，有一行 PATH=$PATH:$HOME/bin，将其修改为 PATH=$PATH:$HOME/bin:[Node.js路径]
* 断开并重新连接服务器，使PATH环境变量生效
* 在用户目录输入 node -v，显示版本号，说明配置成功