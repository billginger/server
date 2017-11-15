# CentOS 常用命令

## 下载

```bash
wget https://nodejs.org/dist/v8.9.1/node-v8.9.1-linux-x64.tar.xz
```

## 解压

```bash
tar -xvf node-v8.9.1-linux-x64.tar.xz
```

## 重命名目录

```bash
mv node-v8.9.1-linux-x64 node
```

## 新建文件

```bash
touch web.json
```

## 修改文本文件

```bash
vi .bash_profile
```

## 删除目录及该目录下所有子目录和文件，且不需确认（慎用）

```bash
rm -rf node_modules
```

## 查看文件内容，支持翻页查看

```bash
less config.json
```

## 安装软件

```bash
yum -y install git-core
```

## 查看 CentOS 系统版本

```bash
cat /etc/redhat-release
```

## 按关键词查询软件

```bash
rpm -qa | grep <关键字>
```

## 查看内存使用量和交换区使用量

```bash
free -m
```

## 查看各分区使用情况

```bash
df -h
```

## 查看所有进程

```bash
ps -ef
```

## 查看所有监听端口

```bash
netstat -lntp
```

## 改变 MongoDB 访问端口

```bash
firewall-cmd --list-all
firewall-cmd --permanent --remove-port=27017/tcp
firewall-cmd --permanent --add-port=27082/tcp
firewall-cmd --reload
```

## 上传文件（在本地目录操作）

```bash
scp web.json root@szx.thinkchina.com.au:/bill/site/
```

## 下载文件（在本地目录操作）

```bash
scp root@szx.thinkchina.com.au:/bill/site/web.json ./
```
