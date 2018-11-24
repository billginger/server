# Docker Nginx on CentOS

## Pull Image

`docker pull nginx`

## Exposing external port

`docker run --name nginx -d -p 8080:80 nginx`

## 建立本地目录

`mkdir -p ~/nginx/conf ~/nginx/logs ~/nginx/www`

## 从 Docker 中拷出配置文件

```r
docker cp nginx:/etc/nginx/nginx.conf ~/nginx/conf/nginx.conf
docker cp nginx:/etc/nginx/mime.types ~/nginx/conf/mime.types
docker cp nginx:/etc/nginx/conf.d ~/nginx/conf/conf.d
```

## 从 Docker 中拷出 HTML 文件

```r
docker cp nginx:/usr/share/nginx/html/index.html ~/nginx/www
docker cp nginx:/usr/share/nginx/html/50x.html ~/nginx/www
```

## 强制移除原来的容器

`docker rm -f nginx`

## 以挂载本地目录和配置文件的方式再次运行容器

```r
docker run --name nginx -d -p 8080:80 -v ~/nginx/www:/www -v ~/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v ~/nginx/logs:/wwwlogs nginx
```

## 编辑配置文件

```nginx

user  nginx;
worker_processes  1;

error_log  /wwwlogs/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /wwwlogs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;
        #access_log  /var/log/nginx/host.access.log  main;

        location / {
            root   /www;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /www;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}
    }
}

```

## 重启 Docker 容器

`docker restart nginx`
