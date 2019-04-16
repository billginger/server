# CentOS 常用命令

## 下载

```
wget https://nodejs.org/dist/v8.9.1/node-v8.9.1-linux-x64.tar.xz
```

## 解压

```
tar -xvf node-v8.9.1-linux-x64.tar.xz
```

## 压缩目录

```
tar zcvf pem.tar.gz pem
```

## 重命名目录

```
mv node-v8.9.1-linux-x64 node
```

## 设置目录的权限

```
chmod -R 777 node_modules
```

## 新建文件

```
touch web.json
```

## 修改文本文件

```
vi .bash_profile
```

## 删除目录及该目录下所有子目录和文件，且不需确认（慎用）

```
rm -rf node_modules
```

## 查看文件内容，支持翻页查看

```
less config.json
```

## 查看文件最后 10 行，循环读取

```
tail -f notes.log
```

## 安装 Git

```
yum -y install git-core
```

## 安装 lrzsz

```
yum -y install lrzsz
```

## 生成 SSH-Key

```
ssh-keygen -t rsa -C "Bill"
```

## 查看 CentOS 系统版本

```
cat /etc/redhat-release
```

## 按关键词查询软件

```
rpm -qa | grep <关键字>
```

## 按关键词查询日志

```
grep 'H5 error: Siebel' lhkwmp_err-0.log
```

## 查看内存使用量和交换区使用量

```
free -m
```

## 查看所有进程

```
ps -ef
```

## 查看所有监听端口

```
netstat -lntp
```

## 获取 firewalld 状态

```
firewall-cmd --state
```

## 改变 MongoDB 访问端口

```
firewall-cmd --list-all
firewall-cmd --permanent --remove-port=27017/tcp
firewall-cmd --permanent --add-port=27082/tcp
firewall-cmd --reload
```

## CentOS7 修改主机名

```
hostnamectl set-hostname xxx
```

## 上传文件（在本地目录操作）

```
scp web.json username@servername:/bill/site/
```

## 下载文件（在本地目录操作）

```
scp username@servername:/bill/site/web.json ./
```

## 上传目录（在本地目录操作）

```
scp -r local_dir username@servername:remote_dir
```

## 下载目录（在本地目录操作）

```
scp -r username@servername:remote_dir local_dir
```

## 使用 Get 方法测试 HTTP 服务

```
curl -X GET "localhost:3020/facebook/webhook?hub.verify_token=abc&hub.challenge=CHALLENGE_ACCEPTED&hub.mode=subscribe"
```

## 使用 Post 方法测试 HTTP 服务

```
curl -H "Content-Type: application/json" -X POST "localhost:3020/facebook/webhook" -d '{"object": "page", "entry": [{"messaging": [{"message": "TEST_MESSAGE"}]}]}'
```
