# Docker Nginx on CentOS

## Pull Image

`docker pull nginx`

## Exposing external port

`docker run --name nginx -d -p 8080:80 nginx`

## 建立本地目录

`mkdir -p ~/nginx/www ~/nginx/logs ~/nginx/conf`

## 从 Docker 中拷出配置文件

`docker cp nginx:/etc/nginx/nginx.conf ~/nginx/conf/nginx.conf`

## 强制移除原来的容器

`docker rm -f nginx`

## 以挂载本地目录和配置文件的方式再次运行容器

`docker run --name nginx -d -p 8080:80 -v ~/nginx/www:/www -v ~/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v ~/nginx/logs:/wwwlogs nginx`
