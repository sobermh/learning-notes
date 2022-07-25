`摘取自菜鸟教程、白月黑羽、`
# Django概述
- Django 采用了 MVT 的软件设计模式，即模型（Model），视图（View）和模板（Template）。
    1. 建议图： 
    ![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722154230.png)
    2. 用户操作流程图：
    ![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722154403.png)
-  Django 本身基于 MVC 模型，即 Model（模型）+ View（视图）+ Controller（控制器）设计模式
    - 优势：
        - 低耦合
        - 开发快捷
        - 部署方便
        - 可重用性高
        - 维护成本低。。。。。。
    1. 简易图
        ![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722153830.png)
    2. 
        ![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722154009.png)
# 安装django
pip install django
script：pip.exe\django-admin.exe
[创建django项目中的文件和文件夹]
lib：内置模块:openpyxl\django\time\flask
# 创建项目
1.打开终端
2.进入某个目录（项目放在哪里）
3.执行命令创建项目 
```
django-admin startproject myproject
#此处myproject为项目名
```
# 创建应用
cd 到项目所在目录，即与manage.py同级，输入如下指令来创建应用：
```
python manage.py startapp users
#blog为应用名
```
## 解析项目应用文件
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722165757.png)
- manage.py 是一个工具脚本，用作项目管理的。会使用它执行管理操作。

- 里面的 mydjangowebsite/ 目录是python包。 里面包含项目的重要配置文件。这个目录名字不能随便改，因为manage.py 要用到它。

- mydjangowebsite/settings.py 是 Django 项目的配置文件. 包含了非常重要的配置项，以后我们可能需要修改里面的配置。

- mydjangowebsite/urls.py 里面存放了 一张表， 声明了前端发过来的各种http请求，分别由哪些函数处理. 

- mydjangowebsite/wsgi.py
要了解这个文件的作用， 我们必须明白wsgi 是什么意思：python 组织制定了 web 服务网关接口（Web Server Gateway Interface） 规范 ，简称wsgi。参考文档 https://www.python.org/dev/peps/pep-3333/
遵循wsgi规范的 web后端系统， 我们可以理解为 由两个部分组成wsgi web server 和 wsgi web application它们通常是运行在一个python进程中的两个模块，或者说两个子系统。`wsgi web server(`**提供高效的http请求处理环境**`) 接受到前端的http请求后，会调用 wsgi web application (`**处理 业务逻辑**`)的接口（ 比如函数或者类方法）方法，由wsgi web application 具体处理该请求。然后再把处理结果返回给 wsgi web server， wsgi web server再返回给前端。`
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220722170545.png)
# 运行Django
python manage.py runserver 3344（默认是8000）
# Django搭建一个博客
