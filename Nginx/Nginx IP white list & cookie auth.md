# Nginx IP 白名单和 Cookie 验证

本文以一个 Nginx 初学者的角度来探索如何实现 Nginx IP 白名单和 Cookie 验证。

## 声明变量

pending

## 判断语句

Nginx 的判断语句通常使用 HttpRewrite 模块来实现，HttpRewrite 是 Nginx 的基本模块，无需另外安装。

使用 [http_rewrite_module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html)：

__if__
* 使用环境:	server, location
> 这里要特别注意“使用环境”，正如 if 只能放到 server 和 location 中那样，放到 if 语句中的指令，使用环境也必须包括 if。
> 另外，HttpRewrite 的 if 不支持嵌套，其实更像 JavaScript 中的 switch。

__break__
* 使用环境:	server, location, if
> break 用来跳出判断语句。准确的说，是跳出所有 HttpRewrite 的语句。

## 获取客户端 IP

`remote_addr`

## 获取客户端 Cookie

`$COOKIE_name`

## 设置客户端 Cookie

使用 [ngx_http_userid_module](http://nginx.org/en/docs/http/ngx_http_userid_module.html)：

```
userid         on; 
userid_name    uid;
userid_domain  example.com;
userid_path    /;
userid_expires 365d;
```

说明：

__userid__
* 默认值：off
* 使用环境：http, server, location
* 值：
  * on: 开启，允许使用版本2的cookie以及记录他们。
  * v1: 允许使用版本1的cookie以及记录他们。
  * log: 不发送cookie，但是写下来记录。
  * off: 禁止发送及写cookie。

__userid_name__
* 设置 cookie 的名称
* 使用环境：http, server, location
* 通过以下方法实现设置 cookie 的值：
  * 值为字符串：`userid_name uid=myCookieValue`
  * 值为变量：`userid_name uid=$trueValue`
  * 同源原则：add_header指令中的domain字段应对应虚拟主机配置的域名。

## nginx.conf

```nginx
user  nginx;
worker_processes  auto;

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

        include  /etc/nginx/ip.conf;
        include  /etc/nginx/cookie.conf;

        location / {
            if ($remote_addr = 182.40.247.145) {
                proxy_pass  http://www.thompsons.cn;
                break;
            }
            if ($COOKIE_uid ~ test) {
                proxy_pass  http://www.thompsons.cn;
                break;
            }
            proxy_pass  http://www.thursdayplantation.net.cn;
        }
    }
}
```

## ip.conf

pending

## cookie.conf

pending
