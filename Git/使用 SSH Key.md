# 使用 SSH Key

## 创建 SSH Key

在 Mac 或 Linux 环境下，在终端中执行以下命令：

`ssh-keygen -t rsa -C "Bill"`

一直回车。创建完成后，进入用户目录下的 .ssh 目录，打印 id_rsa.pub 文件：

`cat id_rsa.pub`

复制打印出来的字符到 Github。

## 对于非 id_rsa.pub 文件

有时我们的 SSH Key 文件不是以 id_rsa.pub 命名的，无法使用 SSH 推送，需要在终端中先执行以下命令：

```
ssh-add -K ~/.ssh/tctt-Bitbucket
```
