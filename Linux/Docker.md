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

更多信息可参考：https://store.docker.com/images/mysql

## 运行 WordPress

`docker run --name wordpress --link mysql:mysql -p 80:80 -d wordpress`

启动 WordPress 容器时可以指定的一些环境参数包括：

```
-e WORDPRESS_DB_USER=... 缺省为 “root”
-e WORDPRESS_DB_PASSWORD=... 缺省为连接 mysql 容器的环境变量 MYSQL_ROOT_PASSWORD 的值
-e WORDPRESS_DB_NAME=... 缺省为 “wordpress”
认证信息：缺省为随机 sha1 串
-e WORDPRESS_AUTH_KEY=...
-e WORDPRESS_SECURE_AUTH_KEY=...
-e WORDPRESS_LOGGED_IN_KEY=...
-e WORDPRESS_NONCE_KEY=...
-e WORDPRESS_AUTH_SALT=...
-e WORDPRESS_SECURE_AUTH_SALT=...
-e WORDPRESS_LOGGED_IN_SALT=...
-e WORDPRESS_NONCE_SALT=...
```
WordPress 默认使用 80 端口，如 80 端口已被占用，可以映射别的端口，比如：

`docker run --name docker_wordpress --link mysql_wordpress:mysql -p 8080:80 -d wordpress`

## 查看实时日志

`docker logs -f -t --since="2018-01-01" --tail=10 wordpress`

--since : 此参数指定了输出日志开始日期，即只输出指定日期之后的日志。

-f : 查看实时日志

-t : 查看日志产生的日期

-tail=10 : 查看最后的10条日志。

wordpress : 容器名称（必须）

## 安装一个 Alpine 版本的 PHP 环境

`docker pull registry.docker-cn.com/library/php:7.2-fpm-alpine`
