# 环境搭建
## 安装JDK
1. 安装下载JDK，配置环境变量JAVA_HOME,变量值填写jdk安装目录
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718113923.png)
2. 在PATH中添加%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin；
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718114434.png)
3. 新建CLASSPATH,变量值填写%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718114757.png)
4. 检验是否配置完成，cmd
```
C:\Users\PC>java -version
java version "17.0.1" 2021-10-19 LTS
Java(TM) SE Runtime Environment (build 17.0.1+12-LTS-39)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.1+12-LTS-39, mixed mode, sharing)
```
## 安装andriod sdk
1. 下载安装
2. 环境变量ANDRIOD_HOME ,变量值是sdk的实际安装路径
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718115306.png)
3. PATH路径加，%ANDRIOD_HOME%\tools;%ANDRIOD_HOME%\platform-tools;%ANDRIOD_HOME%\build-tools\29.0.3;
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718115337.png)
4. 验证是否安装完成
```
C:\Users\PC>adb
Android Debug Bridge version 1.0.41
Version 29.0.6-6198805
Installed as E:\sdk\platform-tools\adb.exe
```
## 安装appium server\
1. http://appium.io/ 安装appium
2. https://nodejs.org/en/download/ 安装nodejs  node -v验证
## 真机授权
1. 手机打开开发者模式，勾选usb调试
2. cmd输入adb devices -l，查看是否有连接电脑的手机

## 安装python第三方库
pip install appium-python-client
# adb
## 构成和工作原理
构成：
- client端，在电脑端，负责发送adb命令
- daemon守护进程，在手机上，负责接收和执行adb命令
- server端，在电脑上，负责管理client和daemon之间的通信
工作原理：
1. client端将命令发送给server端
2. server端就会将命令发送给daemon
3. daemon端进行执行
4. 将执行结果返回给server端
5. server端将结果再返回给client端
## adb常用命令
### 获取包名和界面名
包名（packpage）：决定程序的唯一性
界面名（activity）：一个界面名决定一个界面
- 查看连接的Android版本号
```
adb shell getprop ro.build.version.release
```
- 查看连接的测试手机信息
```
adb devices -l
```
- `查看包名和界面名`
```
C:\Users\PC>adb shell dumpsys activity | findstr "mResume"
    mResumedActivity: ActivityRecord{d162fe2 u0 com.tencent.mm/.ui.LauncherUI t88}
```
### 文件传输
- 发送文件到手机
adb push 电脑文件的路径 手机文件夹的路径

# appium
## appium启动app
1. 电脑打开appium，点击start Server
2. 出现如下页面，再点击“Start Inspector Session”按钮
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718150001.png)
3. 输入获取的配置内容，点击“Start Session”按钮（可先点击3所指的按钮保存，下次直接选择即可）
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220718150104.png)
```
{
  "platformName": "Android",
  "platformVersion": "10",
  "deviceName": "Redmi_7A",
  "appPackage": "com.tencent.mm",
  "appActivity": ".ui.LauncherUI",
  "noReset": true,    
  "fullReset": false
}
```
注意： 
-  小米手机插卡才可以实现usb调试权限的启动，使用安装之后，就可以把卡取走了。
- #解决微信登录，清空之前的记录的问题，必须加上"noReset": true,这一参数。
# 运行python项目
