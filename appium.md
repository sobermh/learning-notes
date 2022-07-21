# 环境搭建
## 安装nodejs
http://nodejs.cn/
因为appium这个工具的服务端是由nodejs语言开发的
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
3. 关闭小米的usb安装提示`发者选项中 -> 启动MIUI优化 ->关闭——我只操作了这个，就可以了。`
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
## 注意
`新版的appiumserver和inspector是分开的，需要单独下载，且需要加一个参数`
![](https://maowansen.oss-cn-hangzhou.aliyuncs.com/img/20220719164944.png)
# 元素的定位
- uiautomatorviewer，android自带的工具，在sdk/tools下（java8及以下，android 8.0以上不支持截屏）
- Weditor 
  1. python-uiautomator2，pip install --pre -U uiautomator2
  2. python -m uiautomator2 init
  3. pip install weditor
  确认安装：cmd-  weditor --help
- appium自带的
## `Html5 webview元素定位工具的实现`
- chrome://inspect/#devices 需要fq
- '下载使用'https://dev.ucweb.com/ uc开发者工具
  1. 需要在C:\Program Files\Appium Server GUI\resources\app\node_modules\appium\node_modules\appium-chromedriver\chromedriver\win加上一个与chrome内核相匹配的chromedriver,`打开公众号和打开小程序的chromedirver的版本可能是不同的，这样会导致打开h5页面和小程序不能同时进行。必须保证chrome版本都一样，才能实现一起运行。有的时候会抽风`
  2. 
## appium

`注意`：
- 重复执行测试用例
  1. pip install pytest -repeat
  2. 方法一：使用注解方式，实现重复执行单条用例
  在测试用例前添加注解@pytest.mark.repeat(value)，value表示重复的次数，来实现单条用例的重复执行。
  ```python
   @pytest.mark.repeat(2)
  ```
  3. 方法二：使用命令函参数，实现重复执行所有用例
  在终端传入-count的方式实现重复执行测试用例
  ```
  # 在终端(terminal)输入：
  pytest -s -v --count=2 test_Pytest.py
  ```
  -s：表示输出用例中的调式信息，比如print的打印信息等。
- 失败用例重跑`（不知道为什么第二次试的时候直接报错，解决办法先搁置了）`
  1. pip install pytest-rerunfailures
  2.方法一：通过注解的形式实现失败重运行
  ```python
   # 用例失败后重新运行2次，重运行之间的间隔时间为10s
    @pytest.mark.flaky(reruns=2, reruns_delay=10)
  ```
  3. 方法二：通过使用命令行参数，实现失败重运行
  ```shell
  # 用例失败后重新运行2次，重运行之间的间隔时间为10s
  # 在终端(terminal)输入：
  pytest -s -v --reruns=2 --reruns-delay=10 test.py
  ```
  4. 重复执行测试用例直到失败停止
  ```
  # 重复运行5次，运行过程中第一次失败时就停止运行
  # 在终端(terminal)输入：
  pytest -s -v --count=5 -x test.py
  ```
- Appium Error: Cannot find any free port in range 8200..8299
  解决办法：adb forward --remove-all 