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

```
docker run -p 3309:3306 --name mysql -v ~/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```
