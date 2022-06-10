# 快速搭建网站
    pip install flask

# html基础知识

<div> </div>自己占一行,块级标签
<span>自己多大就占多大，行内标签
<a href="......." target="_blank">文本</a>超链接文本,在新的页面打开
<img src="......" />(引用别人的图片可能无法显示，被添加了防盗链)
    显示自己的图片，flask的话创建static目录，用于存放图片
块级标签可以嵌套行内标签，行内嵌套行内
列表                  有序列表
<ul>                   <ol>
    <li></li>             <li></li>
    <li></li>             <li></li>
    <li></li>             <li></li>
</ul>                   </ol>

表格
<table border=1>
    <thead>
        <tr> <th>姓名</th> <th>年龄</th> </tr>表头
    </thead>
    <tbody>
        <tr>  <td>zhangsan</td> <td>18</td> </tr>内容
        <tr>  <td>lisi</td>     <td>1</td> </tr>
    </tbody>
</table>

## input系列
<input type="text"/>
<input type="password"/>密码框
<input type="file"/>选择文件框
单选框：name的值保持一致
<input type="radio" name="n1">男
<input type="radio" name="n1">女

<input type="checkbox">复选框

<input type="button" value="提交">普通按钮
<input type="submit" value="提交">提交表单按钮

## 下拉框
<select>
    <option>北京</option>
    <option>上海</option>
</select>
多选
<select multiple>
    <option>北京</option>
    <option>上海</option>
</select>

## 多行文本
<textarea> </textarea>

## 网络请求及表单提交

url-回车
浏览器会发送数据过去，本质上发送的是字符串：
"GET /index http1.1\r\nhost:...\r\nuser-agent\r\n..\r\n\r\n"
"GET /index http1.1\r\nhost:...\r\nuser-agent\r\n..\r\n\r\n数据库"
请求方法：
GET:会显示在url后面
POST:数据更安全，不会体现在URL中，在请求体中。

页面上的数据提交到后台：
页面上的数据，需要使用<form>包裹需要提交的数据
提交的方式：method=“get”
提交的地址：action=“xx/xxxx/xx”
在from标签里面必须有一个submit标签
！！！！！！！！！！！！！！！
在from里面的标签：
每一种需要提交内容的标签，一定要写name属性，就像构建一个字典，{“pwd”：。。。。。}
针对单选或多选等等，最好每一个选项带上一个value值

## 注册案例
1.创建项目
2.创建flask代码，创建static，放静态文件css，jpg
    根据method的不同，对相同的.route()做一个区分。默认支持get方法
    @app.route("/register",methods=["POST","GET"])if..else...

## 总结
1.称呼：
    html--超文本传输语言（与浏览器搭配）。
2.html标签（默认格式样式，以后可以改）
3.html与编程语言无关

# css基础知识
1.直接在标签上写
2.在head标签中写style标签：点加名字
    <style>.name{color:red}</style>
    在下面标签中直接引用：class='c1'
3.写在文件中：在head中写
    <link rel="stylesheet" href="commons.css"/>
    文件中写：.name{color:red；}    .name2{color:red；}
    在下面标签中直接引用：class='name'

## css在flask中的案例
    1.在static中创建commons.css的文件，写上.name{color:red；} 
    2.然后在使用的html文件的head最后写上<link rel="stylesheet" href="/static/commons.css">
    3.在需要使用的标签中使用class=“name”
## css选择器
    id选择器：#name{color:red；}   找id=“name”
    类选择器：.name{color:red；}   找class=“name”
    标签选择器：.div{color:red；}   找<div>
    属性选择器：根据属性去匹配
    后代选择器：
    <!-- 注意 -->：
    下面的会覆盖上面的
    上面的不会被覆盖，加 !important
## 样式
    1.高度和宽度height，width，border（px，宽带支持百分比）
        行内标签：默认无效
        块级标签：默认有效，但别的区域空着也不让用
    2.行内和块级：
        加上display：inline-block既具有行内又具有块级的特性
        display：inline变成行内标签
        display：block变成块级标签
    3.字体和颜色
        color：rgb/red；
        font-size：60px；
        font-weight：600；
        font-family：Microsoft yahei；
    4.文字的对齐方式
        text-align：center 水平居中
        line-height：59px 水平居中
    5.浮动
        style=“float：right”放右边（解决div不那么霸道）
        但是要在最后把他拉回来：
        <div style="clear:both;"></div>
    6.边框居中：margin-left:auto;
            margin-right:auto;
            margin-top:200px;
# BootStrap（插件）
1.下载BootStrap：直接搜BootStrap，下载生成环境
2.使用
    在页面上引入BootStrap
    编写HTML时，按照BootSrtap的规定来编写+自定制
    放入/static/plugins/bootstrap
    导入插件，使用开发版本<link rel="stylesheet" href="/static/plugins/bootstrap-3.4.1/css/bootstrap.css">
    按照bootstrap中的全局css样式，复制修改就可以
## bootstrap动态效果解锁
    bootstrap依赖JavaScript的类库，jQuery
    1.下载jQuery，在页面上应用上jQuery
        直接搜jQuery，下载压缩版compressed，（另存为）
        放到js目录中
    2.在页面上应用bootstrap的javascript类库
        放在</body>上面
        依赖于
        <script src="static/javascript/jquery-3.6.0.min.js"></script>
        动态效果
        <script src="/static/plugins/bootstrap-3.4.1/js/bootstrap.min.js"></script>
# JavaScript
    编程语言，浏览器就是JavaScript语言的解释器
    让程序实现动态效果
## js代码位置
    1.在<title>后面，css代码前
    <script type="text/javascript"> 编写的JavaScript代码</script>
    导入：<script src="/static/my.js"></script>
    2.在</body>前面的最尾部（推荐）
    <script type="text/javascript"> 编写的JavaScript代码</script>
    导入：<script src="/static/my.js"></script>
## 注释
    1.html： <!--注释内容 -->   
    2.css: /*注释内容*/         只能放在style代码块
    3.javascript:               只能放在script代码块
    //注释内容
    /*注释内容*/
## 变量
    var name="俞琦";
## 输出
    console.log(name)
## 字符串类型
    //声明
    var name=" 俞琦"：
    var name=String("俞琦");
    //常见功能
    var v1=name.lenth();
    var v2=name[0]; name.charAt(3)
    var v3=name.trim();去除空白
    var v4=name.substring(0,2);前取后不取
## web动态字符串案例
    <span id="txt">杭州欢迎您的到来</span>
    <script type="text/javascript">
        function show(){
            // 1.去html中找到某个标签并获取他的内容 （DOM）
            var tag = document.getElementById("txt");
            var dataString =tag.innerText;
            console.log(dataString);
            // 2.动态起来，把文本中的第一个字符放在字符串的最后面
            var firstChar =dataString[0];
            var otherString =dataString.substring(1,dataString.lenth);
            var newText= otherString+firstChar;
            console.log(newText);
            // 3.在html标签中更新内容
            tag.innerText=newText;
        }
        //js中的定时器,如：每1s执行一次show函数。
        setInterval(show,1000);
    </script>
## 数组
    //定义
    var v1=[11,22,33,44];
    var v2=array([11,22,33]);

    //操作
    增
        v1[0]="俞琦";
        v1.push("俞琦");在尾部追加
        v1.unshift("俞琦");头部追加
        v1.splice(索引,0,元素);  v1.splice(1,0,"俞琦")  [11,俞琦，22，33，44]
    删
        v1.pop() 尾部删除
        v1.shift() 头部删除
        v1.splice(索引位置,1)   v1.splice(2,1) 索引为2的元素删除[11,22,44];
    循环
        for(var item in v1){
            //item=0/1/2/3  data=v1[item]
        }循环的是索引
        for(var i=0;i<v1.length>;i++){

        }
## 对象（字典）
    info={
        "name":"俞琦",
        "age":18
    }
    info={
        name:"俞琦",
        age:18
    }
    info["name"]="哈哈" 对应加引号的key
    info.name="哈哈" 对应不加引号的key
    循环
        for(var key in info){
            data=info[key]
        }循环的是key
## 条件语句
    与c一致
## 函数
    function func(){
        ...
    }
    func()

    DOM和BOM:内置模块
    jQuery：第三方模块
# DOM
    DOM就是一个模块，模块可以对html页面中的标签进行操作
    //根据id获取标签
        var tag=document.getElementById("id_value");
    //获取标签中的文本
        tag.innerText
    //修改标签中的文本
        tag.innerText="俞琦";
    //创建标签<div>俞琦</div>
        var tag=document.createElement("div");
        //写入内容
        tag.innerText="俞琦"
    //将创建的<li>标签和内容插入<ul>
        1.获取<ul>标签
        2.创建<li>
        3.写入内容
        4.插入到<ul>tag.appendChild(newTag);
## 事件的绑定
    <input>标签button中添加：
    onclick="函数名（）"  单击触发
    获取input框的内容并添加：
        1.找到输入的标签
        2.获取input框中用户输入的内容，并判断不为空
            var newstring=xxxx.value;
            判断:if(newstring.length>0){....}else{alert("输入不能为空")}
        3.创建要添加的标签
            newtag.innerText=newstring;
        4.讲标签添加进ul中
            获取父标签，然后appendchild；
        5.将input框清空
            xxx.value= “ ”；
## 注意
    DOM可以实现很多功能，但是比较繁琐
    页面上的效果：jQuery、vue.js、react.js

# python知识点回顾
## 编码相关
    文件存储时，使用某种编码，打开时需要使用相同的编码，否则会乱码
    字符底层存储时本质上都是二进制
    字符和二进制的对应关系：
        ascll编码，256种对应关系
        gb2312，gbk（中文和亚洲的一些国家）中文：占2个字节
        unicode，ucs2/ucs4（包括所有文明）
        utf-8，中文：占三个字节
    python默认解释器编码（utf-8）
        python.exe 代码文件

## 计算机中的单位
    8位=1字节
## 字符串格式化
    v1="我是{}".format（“俞琦”）
    v2="我是%s"%（“俞琦”）
    name="俞琦"   v3=f"我是{name}"
## 数据类型
    int、bool、str、list、tuple、dict、set、float、None
    转为bool为False：空、None、0
    可变类型和不可变：
        可变：list、set、dict
    可哈希和不可哈希：
        不可哈希：list、set、dict
    字典的键/集合的元素，必须是可哈希类型（list、set、dict不能做字典的键和集合的元素）
    str：
        独有功能:split、upper、lower、startwith、strip、join
        注意：str不可变，不会对原子符进行修改，直接生成新的内容
    list：
        独：append/insert/remove/pop
        注意：list可变，对原数据进行操作
    dict：
        独：get\keys\items\value
## 运算符
    特殊的逻辑运算符：(整体结果取决于谁？)
        v1=99 and 88     #88
        v2=[] or 10      #10
        v3= 10 or []     #10
## 推导式
    data =[i for i in range(10) if i<5>]  #[0,1,2,3,4]
## 函数
    定义：
    参数：位置传参/关键字传参/参数默认值/动态参数*args，**kwargs
    返回值
        函数没有返回值默认返回None
    函数的进阶：
        python中是以函数为作用域。
        全局变量（大写）、局部变量（小写）
        局部变量中global关键字，引用全局的变量（不是局部新建的）
    内置函数;
        bin\hex\odc\max\min\dicmod\sorted\open文件操作
## 文件操作：
    with open自动关闭
    打开的模式：
        r：读        【文件不存在，报错】     【文件夹不存在，报错】
        w：写（清空）【文件不存在，自动新建】   【文件夹不存在，报错】
        a：追加      【文件不存在，自动新建】   【文件夹不存在，报错】
    注意：os.makedirs/os.path.exsits是否存在，不存在新建目录
## 模块
    1.自定义模块:
    2.内置模块：
        time/datatime/json/re/random/os..
    查看当前目录下所有文件:os.listdir/os.walk
    关于时间模块：时间戳/datetime/字符串可以互相转换
    关于json模块：
        json本质是字符串，有一些自己格式的要求，如：无元组、无单引号
        json.dumps序列化时，只能序列化python常用数据类型
    关于re正则模块：
        正则：\d \w
        默认贪婪，不贪婪加？
        re.search/re.match/re.findall
    3.第三方模块:
        requests/openpyxl/python-docx/flask...
## 面向对象
    三大特性：封装、继承、多态
# 前端知识回顾
    html：
        div 默认块级标签，span默认行内标签
        from+input/select/textarea
            action：提交地址
            methond：提交方式
            必须有submit
            内部标签必须设设置name属性
    css：
        内边距：padding
        外边距：margin
        局部一定会用到：div+float（脱离文档流，clear：both；clearfix）
        hover，鼠标放上去就会触发的css样式
# jQuery
    jQuery是JavaScript的第三方模块
        基于jQuery，自己开发一个功能
        现成的工具依赖jQuery，例如：bootstrap动态效果
##  快速上手
    <h1 id="txt">汇健科技</h1>
    <script src="/static/javascript/jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        //利用jquery中的功能实现某种效果
        $("#txt").text("汇馨传感");
    </script>
## 寻找标签(直接寻找)
    id:
        $("#txt")
    样式选择器:
        $(".c1")
    标签选择器；
        $("h1")
    层级选择器:
        $(".c1 .c2 a")
    多选择器：
        $("#c3 ,#c2 ,li")
    属性选择器:
        $("input[name="n1"]")
## 寻找标签（间接寻找）
    找到上一个兄弟
    ........
# MYSQL
    查看已有数据库：
        show databases；
    创建数据库：
        create database 数据库名字 default charset utf8 collate utf8_general_ci;
    删除数据库：
        drop database 数据库名字；
    进入数据库（进入文件夹）
        use 数据库名字；
    查看文件夹下所有的数据表（文件）:
        show tables；
## 数据表的管理（文件）
    创建表：
        create table user(
        user_id  int  not null primary keyauto_increment,                       
        username varchar(16)  not null,  
        password char(8)      not null,      
        sexy     char(4)      not null
        )default charset=utf8;
    查看表详细信息：desc 表名称;
    查看表：select * from 表名称；
    删除表：
        drop table 表名称;
    插入数据：
        insert into 表名（字段名1，字段名2） values （1000，18）；
        insert into 表名（字段名1，字段名2） values （1000，18），（133，55）；
## 常用数据类型：
整型：
    tinyint：
        有符号，取值范围-128~127【默认】
        无符号，0~255【 tinyint  unsigned】
    int：
        有符号：-2147483648~2147483647
        无符号：....
    bigint

小数：
    float
    double
    decimal：
        准确的小数值，m是数字总个数（负号不算），d是小数点后个数，m最大值65，d最大30
        如：
            create table 表名称{
                salary decimal（8，2）  不超过8个数字，小数点后2个
            }default charset=utf8；

字符串：
    char（m）：查询速度快 m最大255个字符
        定长字符串：char（11） 固定11个字符串进行存储，哪怕没有11个，也会存储11个
    varchar（m）：节省空间  m最大是65535字节
        变长字符串：varchar（11）
    text（m）： m最大 65535个字符
    mediumtext
    longtext
 
时间：
    datetime：
        YYYY-MM-DD HH:MM:SS
    date：
        YYYY-MM-DD
## 数据行操作
    新增数据：
        insert into 表名（字段名1，字段名2） values （值1，值2），（值1，值2）；
    删除数据：
        delete from 表名；
        delete from 表名 where 条件；id in（1，3）等于id=1 or id=3；
    修改数据：
        update 表名 set 列=值，列=值 where 条件； 
    查询数据：
        select * from 表名称；
        select 字段名，字段名 from 表名称  where 条件；
    
# python操作mysql
     pip install pymysql
     import pymysql
## 插入数据
1.连接mysql
    conn =pymysql.connect(host='127.0.0.1',port=3306,user='root',passwd="123456",charset='utf8',db='users')
    cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)
2.发送指令(切记：！！！！千万不要用字符串格式化去sql拼接，会被sql注入)
    sql = "insert into user(username,password,sexy) values(%s,%s,%s)"
    cursor.execute(sql,["zhangsan","123456","male"])
    # sql = "insert into user(username,password,sexy) values(%(n1)s,%(n2)s,%(n3)s)"
    # cursor.execute(sql,{"n1":"zhangsan","n2":"123456","n3":"female"})

    conn.commit()
3.关闭连接
    cursor.close()
    conn.close()
## 查询数据
 1.连接mysql
    conn =pymysql.connect(host='127.0.0.1',port=3306,user='root',passwd="123456",charset='utf8',db='users')
    cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)
 2.发送指令(切记：！！！！千万不要用字符串格式化去sql拼接，会被sql注入)
    sql = "select * from user where user_id >%s"
    cursor.execute(sql,[1])
    data_list=cursor.fetchall()获取符合条件的所有数据-----没有数据是空列表
    data_list=cursor.fetchone()获取符合条件的第一条数据----没有数据是None
    print(data_list)
    for row_dict in data_list:
        print(row_dict)
    conn.commit()
3.关闭连接
    cursor.close()
    conn.close()
## 删除数据
1.连接mysql
    conn =pymysql.connect(host='127.0.0.1',port=3306,user='root',passwd="123456",charset='utf8',db='users')
    cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)
 2.发送指令(切记：！！！！千万不要用字符串格式化去sql拼接，会被sql注入)
    sql = "delete from user where user_id=%s"
    cursor.execute(sql,[3,])
    conn.commit()
 3.关闭连接
    cursor.close()
    conn.close()
## 修改数据
1.连接mysql
    conn =pymysql.connect(host='127.0.0.1',port=3306,user='root',passwd="123456",charset='utf8',db='users')
    cursor=conn.cursor(cursor=pymysql.cursors.DictCursor)
2.发送指令(切记：！！！！千万不要用字符串格式化去sql拼接，会被sql注入)
    sql = "update user set sexy=%s where username=%s"
    cursor.execute(sql,["female","zhangsan"])
    conn.commit()
3.关闭连接
    cursor.close()
    conn.close()
## 注意！！！！
    查可以没有commit，增、删、改必须要有commit，不然数据库中的数据不会发生改变
    不要用python的字符串格式化进行拼接（会被sql注入），要用execute+参数
# flask+mysql

# django
## django的安装
    pip install django
## 创建项目
    (1)终端django admin startproject 项目名称（推荐）
    (2)pycharm专业版，直接创建，项目的目录不要放在python的安装目录
## 默认文件介绍
项目名
----manage.py         (项目的管理，启动项目，创建app、数据管理)
----项目名文件夹
    ----_init__.py
    ----asgi.py       （接收网络请求）
    ----settings.py   （项目配置）
    ----urls.py       （url和函数的对应关系）
    ----wsgi.py       （接收网络请求）
## app的创建和说明
创建：python manage.py startapp app名
app名
----migrations          （数据库变更记录）
    ----__init__.py
----__init__.py
----admin.py            （django默认提供了admin后台管理）
----apps.py             （app启动类）
----models.py           （对数据库操作）
----tests.py             (单元测试)
----views.py            （函数）
## 快速上手
1.确保app已注册（settings.py）'app名.apps.App01Config'
2.编写url和视图函数对应关系（urls.py）from appname import views
3.编写试图函数（views.py） from django.shortcuts import render,HttpResponse(request)
4.启动django项目
    （1） python manage.py runserver
     (2)直接运行
## 静态文件
1.templates存入html文件
2.static存入图片、css、js、plugins