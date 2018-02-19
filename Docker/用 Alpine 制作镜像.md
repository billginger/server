# 用 Alpine 制作镜像

## 准备基础镜像

拉取 alpine 镜像

`docker pull alpine`

进入 alpine 容器

`docker run -it alpine /bin/sh`

## 对容器进行修改

下载文件

`wget https://download.strongswan.org/strongswan-5.6.1.tar.bz2`

解压文件

`tar -xf strongswan-5.6.1.tar.bz2`

## 对容器进行管理

在容器内退出容器

`exit`

查看正在运行的容器

`docker ps`

查看所有容器

`docker ps -a`

重新进入容器

```
docker start 6f9703e8cc78
docker attach 6f9703e8cc78
```

进入容器，退出时不停止容器

```
docker start 6f9703e8cc78
docker exec -it 6f9703e8cc78 /bin/sh
```

在容器外停止容器

`docker stop 6f9703e8cc78`

删除容器

`docker rm 6f9703e8cc78`

## 提交镜像

从容器创建一个新的镜像

`docker commit 6f9703e8cc78 strongswan:0.1`

按照 Docker Hub 命名规范标记镜像

`docker tag strongswan:0.1 billginger/images:strongswan-0.1`

删除标记前的镜像

`docker rmi strongswan:0.1`

登录 Docker Hub 帐号

`docker login`

推送镜像

`docker push billginger/images:strongswan-0.1`