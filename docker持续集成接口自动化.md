***`目的：使用docker技术，安装一个jenkins，映射一个端口。在客户端访问，配置接口自动化项目环境，进行持续集成。`***
# Docker概述
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220715095358.png)
概念 | 说明
:--|:--
Docker 镜像(Images) | Docker 镜像是用于创建 Docker 容器的模板，比如 Ubuntu 系统|
|Docker 容器(Container)|容器是独立运行的一个或一组应用，是镜像运行时的实体。|
Docker 客户端(Client)|Docker 客户端通过命令行或者其他工具使用 Docker SDK (https://docs.docker.com/develop/sdk/) 与 Docker 的守护进程通信。
Docker 主机(Host) | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。
Docker Registry|Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。<br> Docker Hub(https://hub.docker.com) 提供了庞大的镜像集合供使用。<br>一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。<br>通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本。我们可以通过 <仓库名>:<标签> 的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以 latest 作为默认标签。
Docker Machine|Docker Machine是一个简化Docker安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装Docker，比如VirtualBox、 Digital Ocean、Microsoft Azure。
# Ubuntu安装Docker
参照官网文档进行下载
测试docker是否下载成功：
```shell
root@aliyun:/usr/local/bin# docker version
Client: Docker Engine - Community
 Version:           20.10.17
 API version:       1.41
 Go version:        go1.17.11
 Git commit:        100c701
 Built:             Mon Jun  6 23:02:56 2022
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.17
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.17.11
  Git commit:       a89b842
  Built:            Mon Jun  6 23:01:02 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.6
  GitCommit:        10c12954828e7c7c9b6e0ea9b0c02b01407d3ae1
 runc:
  Version:          1.1.2
  GitCommit:        v1.1.2-0-ga916309
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```
或者运行第一个docker：
```shell
root@aliyun:/usr/local/bin# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:2498fce14358aa50ead0cc6c19990fc6ff866ce72aeb5546e1d59caac3d0d60f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

*出现Hello from Docker!代表成功*

# Docker镜像加速
阿里云镜像获取地址：https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors
，登陆后，左侧菜单选中镜像加速器就可以看到你的专属地址了：
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220715102452.png)

检测是否配置成功：
```
$ docker info
Registry Mirrors:
    https://reg-mirror.qiniu.com
```

#  创建jenkins镜像
## 小白方法
1. 搜索jenkins镜像相关信息
```shell
root@aliyun:/usr/local/bin# docker search jenkins
NAME                           DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
jenkins                        DEPRECATED; use "jenkins/jenkins:lts" instead   5510      [OK]       
jenkins/jenkins                The leading open source automation server       3087                 
jenkins/jnlp-slave             a Jenkins agent which can connect to Jenkins…   150                  [OK]
jenkins/inbound-agent                                                          66                   
bitnami/jenkins                Bitnami Docker Image for Jenkins                53                   [OK]
jenkins/slave                  base image for a Jenkins Agent, which includ…   48                   [OK]
```
2. 参照jenkins官网：https://www.jenkins.io/zh/download/  使用docker pull jenkins/jenkins:lts-jdk11下载镜像
```shell
root@aliyun:/usr/local/bin# docker pull jenkins/jenkins:lts-jdk11
lts-jdk11: Pulling from jenkins/jenkins
647acf3d48c2: Pull complete 
832e288237bc: Pull complete 
ea194d1bd1da: Pull complete 
98569593b9fd: Pull complete ....
```
3. 启动镜像
按照阿里云服务器安全组中开放的端口，配置启动端口
```
root@aliyun:/usr/local/bin# docker run -it -p 3344:8080 jenkins/jenkins:lts-jdk11 
Running from: /usr/share/jenkins/jenkins.war
webroot: EnvVars.masterEnvVars.get("JENKINS_HOME")
2022-07-15 03:03:41.814+0000 [id=1]	INFO	org.eclipse.jetty.util.log.Log#initialized: Logging initialized @1183ms to org.eclipse.jetty.util.log.JavaUtilLog....
```
4.访问配置
- IP+3344访问jenkins成功
- 再打开一个shell面板
```
root@aliyun:~# docker exec -it 4738f0a62349 /bin/bash
jenkins@4738f0a62349:/$ ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
```
- 查看密码：
```
jenkins@4738f0a62349:/$ cat /var/jenkins_home/secrets/initialAdminPassword
```
- 安装插件

### `安装配置python环境`

1. 以root权限进入jenkins容器：
```
root@aliyun:~# docker exec -it -uroot 4738f0a62349 /bin/bash
```
2. 前置安装一些软件包
```
apt-get update # 获取最新的软件包
apt-get upgrade # 升级已安装的软件包
 
# 提前安装，以便接下来的配置操作
 
apt-get -y install gcc automake autoconf libtool make
 
apt-get -y install make*
 
apt-get -y install zlib*
 
apt-get -y install openssl libssl-dev
 
apt-get install sudo
```
注意:
如果在安装make* 报错的话,不需要管他,继续往下安装

3. 安装python3.10.2
```
cd /var/jenkins_home # 进入jenkins的安装目录
mkdir python3   # 新建一个python3目录
cd python3
apt-get -y install wget
wget https://www.python.org/ftp/python/3.10.2/Python-3.10.2.tgz
tar -zxvf Python-3.10.2.tgz
mv Python-3.10.2 py3.10
cd py3.10
```
配置环境变量
```
apt-get -y install vim
vim /etc/profile
#写入以下内容
#Python3.8
export PYTHON_HOME=/var/jenkins_home/python3
export PATH=$PATH:$PYTHON_HOME/bin
------------------------------------------
source /etc/profile
echo $PATH  查看环境是否配置成功
```
```
./configure --prefix=/var/jenkins_home/python3  --with-ssl # 指定安装的目录
make   # 编译
make install  # 安装
```

4. 添加一些软链接：python3 和pip3
```
　ln -s /var/jenkins_home/python3/bin/python3.10  /usr/bin/python3
　ln -s /var/jenkins_home/python3/bin/pip3 /usr/bin/pip3
```
5. 检查配合的环境
```
 python3 -V 和 pip3 -V
```
### 导出配置过的镜像
1. 退出容器 ctrl+p+q
2. 新建一个镜像：docker commit -m="jenkins and python" -a="maowansen" 4738f0a62349 jenkins/python:1.0
3. 上传到aliyun
```
docker login --username=maohui registry.cn-hangzhou.aliyuncs.com
```

```
docker tag 23554f052b7f registry.cn-hangzhou.aliyuncs.com/maowansen/maowanseng-jenkins-python:1.0
```

```
docker push registry.cn-hangzhou.aliyuncs.com/maowansen/maowanseng-jenkins-python:1.0
```
# Jenkins配置
1.创建一个新的任务
- 源码管理，配置gitee的仓库地址，添加Credentials认证信息（注意分支是master还是main）
- 可以配置触发器，定时触发，0 20 * *  3,每个礼拜，礼拜三8点
- linux构建shell脚本：
cd case
python3 run.py
- 生成allure，
需要先下载allure插件，第一个Path为python中写的报告生成的临时文件夹:report/tmp。`注意生成allure报告，需要先下载allure压缩工具包`，
```

apt-get install -y lrzsz
rz **/allure-commandline-2.17.2.zip

unzip allure-commandline-2.17.2.zip
vim /etc/profile
```
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220715172230.png)

```
# 使环境变量生效
source /etc/profile

# allure_pytest是对allure需要的json文件的生成做的一个插件
pip install  allure_pytest
```
然后在系统的全局变量中，添加解压的allure的地址


# docker资源
Docker 官方主页: https://www.docker.com
Docker 官方文档: https://docs.docker.com/
Docker Hub: https://hub.docker.com
阿里云的加速器：https://help.aliyun.com/document_detail/60750.html
