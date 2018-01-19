# Docker 入门

## Docker CE for Mac

https://store.docker.com/editions/community/docker-ce-desktop-mac

## Run it

* Run `docker version` to check that you have the latest release installed.
* Run `docker run hello-world` to verify that Docker is pulling images and running as expected.

## 使用国内镜像加速

`docker pull mysql`

改为

`docker pull registry.docker-cn.com/library/mysql`

## 运行 MySQL

`docker run -p 3309:3306 --name mysql -v ~/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql`

`-p 3309:3306` 是将 docker 的 3306 端口映射到本机 3309 端口

`-v ~/docker/mysql/data:/var/lib/mysql` 是将 docker 的 /var/lib/mysql 目录映射到本机的 ~/docker/mysql/data 目录

`-e MYSQL_ROOT_PASSWORD=123456` 输入密码，mysql 原始密码为 123456

如果需要修改密码 执行 `docker -exec -it 容器id /bin/bash` 进入容器修改密码，修改后可以使用 `docker commit 容器id 新名称` 提交镜像修改

容器启动后，就可以用可视化界面进行连接了。注意暴露的端口是 3309
