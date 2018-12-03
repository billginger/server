# 使用 Node.js 镜像

## Node.js 官方已经推出 Docker 镜像

[Download | Node.js](https://nodejs.org/en/download/)

[Official Node.js Docker Image](https://hub.docker.com/_/node/)

## 快速下载并使用

拉取一个长期支持 Alpine 版：

`docker pull node:lts-alpine`

直接使用镜像运行 Node.js 脚本：

```
docker run -it --rm --name node -v "$PWD":/usr/src/app -w /usr/src/app node:lts-alpine node test.js
```

参数释义：
* -i: 以交互模式运行容器，通常与 -t 同时使用
* -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用
* --rm: 在容器退出时自动清理容器内部的文件系统
* --name: 给容器命名
* -v: 挂载目录
* -w: 工作目录

## 以容器方式使用

运行 Node.js 容器：

```
docker run --name node -v /data:/data -d -p 3000:3000 node:lts-alpine sh -c "while true; do echo 1; sleep 1; done"
```

参数释义：
* -d: 后台运行容器，并返回容器ID
* -p: 端口映射，格式为：主机(宿主)端口:容器端口

镜像名称后面的命令是为了防止容器自动退出。

进入 Node.js 容器：

```
docker exec -it node sh
```

## 封装自己的镜像

创建 Dockerfile 文件：

```
FROM node:lts-alpine

RUN npm install pm2 -g
EXPOSE 3000
CMD tail -f /dev/null
```

制作镜像：

`docker build -t node-with-pm2 .`

运行镜像：

```
docker run --name node -v /data:/data -d -p 3000:3000 node-with-pm2
```

进入容器：

```
docker exec -it node sh
```

## 基于 Nginx 镜像封装

创建 Dockerfile 文件：

```
FROM nginx

ADD node /node
ENV PATH $PATH:/node/bin
RUN npm install pm2 -g
```

制作镜像：

`docker build -t nginx-node-pm2 .`

运行镜像：

```
docker run --name nginx -d -p 80:80 nginx-node-pm2
```

进入容器：

```
docker exec -it nginx bash
```

以挂载本地目录和配置文件的方式运行容器：

```r
docker run --name nginx -d -p 80:80 -v /data/nginx:/etc/nginx nginx
```
