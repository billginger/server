# Docker Hub

## 注册帐号

访问 https://hub.docker.com/

需要翻墙，因为注册时有 Google 人机身份验证。

注册成功后，进行邮件验证，登录帐号。

## 创建仓库

你需要创建一个仓库作为镜像的存储位置。

例如：billginger/images

你可以选择该仓库是公开的，还是私密的。

Docker Hub 允许每个帐号免费创建 1 个私有仓库。

## 提交镜像

在客户端登录帐号

`docker login`

推送镜像

`docker push billginger/images:strongswan-0.1`