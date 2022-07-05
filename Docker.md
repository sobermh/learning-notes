# Docker概述
## Docker的历史
2010，美国人创建了dotCloud
2013，Docker开源
2014，Dcoker1.0发布
Docker优点：
1.虚拟机笨重，Docker容器技术轻巧，但也是虚拟化技术
## 聊聊Docker
Docker基于Go语言开发的
官网：https://www.docker.com/
文档地址：https://docs.docker.com/
仓库地址：https://hub.docker.com/
## Docker和虚拟机的不同
传统虚拟机，虚拟出一条硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件；
容器内的应用直接运行在宿主机的内容，容器是没有自己的内核的，也没有虚拟机的硬件。
## DevOps(开发运维)
更快速的交付和部署
更便捷的升级和扩容
更简单的运维
更高效的计算资源利用
# Docker安装
## Docker的基本组成
![](./assets/1656309067832.jpg)
### 镜像（image）：
docker镜像就好比一个模板，可以通过这个模板来创建容器服务，tomcat镜像===>run===>tomcat01容器（提供服务器），通过这个镜像可以创建多个容器。
### 容器（container）：
Docker利用容器技术，独立运行一个或者一个组应用，通过镜像来创建
目的就可以把这个容器理解为一个简易的linux
### 仓库(repository)：
仓库就是存放镜像的地方
仓库分为私有和公有的
Docker Hub默认是国外的
阿里云...都有容器服务器（配置镜像加速）
## 安装Docker
查看linux系统的内核：
4.15.0-169-generic
查看系统的版本：
cat /etc/os-release

查看官方文档：一步一步的安装

查看是否安装成功： sudo docker version  

验证是否成功运行：sudo docker run hello-world

查看镜像列表：sudo docker images

docker默认工作路径：/var/lib/docker 

## 配置阿里云镜像加速
去阿里云找容器镜像服务
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v9gy47ph.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker

## 回顾run--->HelloWorld工作流程流程
![](./assets/1657010426741.jpg)
## 底层原理
docker是一个client、server结构的系统，docker的守护进程运行在主机上，通过socket从客户端访问
![](./assets/企业微信截图_1657010696418.png)
### docker为什么比vm快
1.docker有着比虚拟机更少的抽象层

2.docker利用的是宿主机的内核，vm需要时guest os

![](./assets/企业微信截图_16570109107024.png)
所以说，新建一个容器的时候，docker不需要像虚拟机一样重新加载一个操作系统内核，避免引导。虚拟机时加载guest os，分钟级别；而docker是利用宿主机的操作系统，省略了这个复杂的过程，秒级！

# Docker命令
## 帮助命令

## 镜像命令
## 容器命令
## 操作命令
# Docker镜像
# 容器数据卷
# DockerFile
# Docker网络原理
# IDEA 整合Docker
# Docker Compose
# Dcoker Swarm
# CI\CD Jenkins

