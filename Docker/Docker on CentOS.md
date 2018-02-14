# Docker on CentOS

## 前提条件

Docker 要求 CentOS 系统的内核版本高于 3.10，通过 uname -r 命令查看你当前的内核版本。

`uname -r`

## 添加 yum 源

Install required packages. yum-utils provides the yum-config-manager utility, and device-mapper-persistent-data and lvm2 are required by the devicemapper storage driver.

`yum install -y yum-utils device-mapper-persistent-data lvm2`

Use the following command to set up the stable repository. You always need the stable repository, even if you want to install builds from the edge or test repositories as well.

`yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

## 使用 yum 安装

查看可安装版本：

`yum list docker-ce --showduplicates | sort -r`

安装最新版的 docker：

`yum install docker-ce`

## 启动 docker

Start Docker.

`systemctl start docker`

Verify that docker is installed correctly by running the hello-world image.

`docker run hello-world`

## 参考资料

https://docs.docker.com/install/linux/docker-ce/centos/