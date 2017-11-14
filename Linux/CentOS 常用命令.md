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

## 删除目录及该目录下所有子目录和文件，且不需确认（慎用）

```bash
rm -rf <目录名>
```

## 查看文件内容，支持翻页查看

```bash
less <文件名>
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
