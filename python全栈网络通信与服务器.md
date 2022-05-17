# 网络概述 
## ip地址
用来标记网络上的一台电脑
linux:ifconfig   sudo ifconfig ens40(网卡) down关闭/up开启   ctrl+a回到命令行行首
                                                            ctrl+e回到命令行行尾
windows:ipconfig
ipv4：256*256*256*256
ipv6:很多
网络号+主机号
## 端口
确认哪个程序（“进程”是运行起来的“程序”）：0-65535 2的16次方
80端口是http服务
21端口是ftp服务
## 私有ip
在局域网使用，不在公网使用
10.0.0.0~10.255.255.255
172.16.0.0~172.31.255.255
192.168.0.0~192.168.255.255

# socket
from socket import *
## udp
    发送数据的流程：                     接收数据的流程：
    1.创建套接字                        1.创建套接字
    2.发送数据                          2.绑定本地自己的信息（ip，port）  
    3.关闭                              3.接收数据
                                        4.关闭
### 创建udp服务端套接字
    udp_serversocket = socket(AF_INET, SOCK_DGRAM)
    # 2.绑定ip和端口号(必须是自己电脑的)
    IP = "127.0.0.1"
    PORT = 3333
    udp_serversocket.bind((IP, PORT))
    while True:
        # 3.接受数据
        BUFLEN = 1024  # 每次最多接收多少字节
        recv_data = udp_serversocket.recvfrom(BUFLEN)  # recvfrom接收的数据是元组，(内容,(源ip+port))
        # 4.打印接收的数据
        recv_msg=recv_data[0] #存储接收的数据
        send_addr=str(recv_data[1]) #存储发送方的地址信息
        print(f'{send_addr}:{recv_msg.decode()}')
        print(recv_data)
    # 5.关闭套接字
    udp_serversocket.close()

### 创建udp客户端套接字（客户端可以先不绑定端口，系统会随机分）
    udp_socket=socket(AF_INET,SOCK_DGRAM)
    #可以使用套接字持续收发数据
    while True:
        content=input('>>>')#内容
        if content=='exit':
            break
        #!!!内容需要转换为二进制才能发送.encode(“默认utf-8”)//b"xxxx"
        IP='127.0.0.1'#服务器ip
        PORT=3333#端口
        #发送内容和连接服务器的ip和端口
        udp_socket.sendto(content.encode("utf-8"),(IP,PORT))
    #关闭套接字
    udp_socket.close()
## tcp
（可靠的，基于连接，稳定的）
### 创建tcp客户端
    #1.创建tcp套接字
    # 实例化一个socket对象，指明协议，ip/tcp
    tcpc_Socket = socket(AF_INET, SOCK_STREAM)

    #2.链接服务器
    #服务端ip和端口
    IP = '127.0.0.1'
    SERVER_PORT = 13333
    BUFLEN = 1024
    # 连接服务端socket
    tcpc_Socket.connect((IP, SERVER_PORT))

    #3.发送数据
    while True:
        # 从终端读入用户输入的字符串
        toSend = input('>>> ')
        if  toSend =='exit':
            break
        # 发送消息，也要编码为 bytes
        tcpc_Socket.send(toSend.encode())
        # 等待接收服务端的消息
        recved = tcpc_Socket.recv(BUFLEN)
        # 如果返回空bytes，表示对方关闭了连接
        if not recved:
            break
        # # 打印读取的信息
        print(recved.decode())

    #4.关闭套接字
    tcpc_Socket.close()
### 创建tcp服务端
    # 1.创建套接字
    # 实例化一个socket对象
    # 参数 AF_INET 表示该socket网络层使用IP协议（ipv4）
    # 参数 SOCK_STREAM 表示该socket传输层使用TCP协议
    listenSocket= socket(AF_INET, SOCK_STREAM)

    # 2.绑定本地信息blid
    # 主机地址为空字符串，表示绑定本机所有网络接口ip地址
    # 等待客户端来连接
    IP = '127.0.0.1'
    # 端口号 9999
    PORT = 13333
    # 定义一次从socket缓冲区最多读入512个字节数据
    BUFLEN = 512
    # socket绑定地址和端口
    listenSocket.bind((IP, PORT))

    # 3.让默认的套接字由主动变为被动listen
    # 使socket处于监听状态，等待客户端的连接请求
    # 参数 128 表示 最多接受多少个等待连接的客户端,处于堵塞状态
    listenSocket.listen(128)
    print(f'服务端启动成功，在{PORT}端口等待客户端连接...')

    # 4.等待客户端的连接
    # 接受客户端的数据,处于堵塞状态
    # (监听套接字负责等待新的客户端进行连接)
    # （accept）产生的新的套接字用来为客户端服务
    dataSocket, client_addr = listenSocket.accept()
    print('接受一个客户端连接:', client_addr)

    #5.接收客户端发送过来的请求
    # netstat -an|find /i "13333"cmd查看13333端口号服务
    # 连接成功的话，有三个，一个是监听，两个是建立连接的客户端和服务端
    global info  # 声明全局变量，将数据传入到flask中
    while True:
        # 尝试读取对方发送的消息
        # BUFLEN 指定从接收缓冲里最多读取多少字节
        recved = dataSocket.recv(BUFLEN)
        # 如果返回空bytes，表示对方关闭了连接
        # 退出循环，结束消息收发
        if not recved:
            break
        # 客户端发送的信息是什么类型的数据，就怎么解码，不一定都是utf8的字符串
        # 读取的字节数据是bytes类型，需要解码为字符串
        info = recved.decode()
        print(f'收到对方信息： {info}')
        #回收客户端数据
        # 服务器接收到之后，告诉客户端接到了，发送的数据类型必须是bytes，所以要编码
        dataSocket.send(f'服务端接收到了信息 {info}'.encode())

    #6.关闭套接字
    # 服务端也调用close()关闭socket
    dataSocket.close()
    listenSocket.close()

### 多用户服务端
    from socket import *
    # 1.创建套接字
    listenSocket= socket(AF_INET, SOCK_STREAM)

    # 2.绑定本地信息bind
    IP = '127.0.0.1'
    PORT = 13333
    BUFLEN = 1024
    listenSocket.bind((IP, PORT))

    # 3.让默认的套接字由主动变为被动listen
    listenSocket.listen(128)
    print(f'服务端启动成功，在{PORT}端口等待客户端连接...')


    #5.接收客户端发送过来的请求
    global info  # 声明全局变量，将数据传入到flask中
    while True:

        # 4.等待客户端的连接
        dataSocket, client_addr = listenSocket.accept()
        print('接受一个客户端连接:', client_addr)
        while True:
            recved = dataSocket.recv(BUFLEN)
            # 如果返回空bytes，表示对方关闭了连接（客户端调用close那么recv（）就会阻塞）
            if not recved:
                break
            info = recved.decode()
            print(f'收到对方信息： {info}')
            dataSocket.send(f'服务端接收到了信息 {info}'.encode())
        dataSocket.close() #表示关闭为一个客户端的服务，accept（）会继续服务

    #6.关闭套接字
    listenSocket.close()#表示关闭一个服务器的服务，accept（）停止服务

### 多任务服务端
#### 线程的基本知识
    并行：真的多任务
    并发：假的多任务
一个程序运行起来之后，一定有一个执行代码的东西，这个东西就称之为线程
    线程的执行没有先后顺序（不知道谁先执行，可通过延时的方式控制）
    如果创建thread时执行的函数，运行结束那么意味着子线程结束了。
    主线程默认最后结束（主线程结束，子线程肯定死了）

    1. #创建实例对象和线程
    import threading
    t2 = threading.Thread(target=函数名)#只是创建了实例对象，没有创建线程
    t2.start()#创建了线程，并启动线程,开始执行
        length=len(threading.enumerate())
        print('当前运行的线程数为：%d'%length)
    2.创建一个类继承threading.Thread的run（self）方法。t=类名（）  t.start（）
#### 多线程共享全局变量
    global
    在一个函数中，对全局变量进行修改的时候，到底是否需要使用global进行说明，要看是否对全局变量的指向进行了修改。
    如果修改了执行，即让全局变量指向了一个新的地方，那么必须使用global。如果，仅仅是修改了指向的空间中的数据，此时不用必须使用global。