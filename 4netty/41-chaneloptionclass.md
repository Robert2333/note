# 4.1 ChanelOption

> [https://www.cnblogs.com/googlemeoften/p/6082785.html](https://www.cnblogs.com/googlemeoften/p/6082785.html)

ChannelOption的各种属性在套接字选项中都有对应

下面简单的总结一下ChannelOption的含义已及使用的场景

### 1、ChannelOption.SO\_BACKLOG

ChannelOption.SO\_BACKLOG对应的是tcp/ip协议listen函数中的backlog参数，函数listen\(int socketfd,int backlog\)用来初始化服务端可连接队列，

服务端处理客户端连接请求是顺序处理的，所以同一时间只能处理一个客户端连接，多个客户端来的时候，服务端将不能处理的客户端连接请求放在队列中等待处理，backlog参数指定了队列的大小

### 2、ChannelOption.SO\_REUSEADDR

ChanneOption.SO\_REUSEADDR对应于套接字选项中的SO\_REUSEADDR，这个参数表示允许重复使用本地地址和端口，

比如，某个服务器进程占用了TCP的80端口进行监听，此时再次监听该端口就会返回错误，使用该参数就可以解决问题，该参数允许共用该端口，这个在服务器程序中比较常使用，

比如某个进程非正常退出，该程序占用的端口可能要被占用一段时间才能允许其他进程使用，而且程序死掉以后，内核一需要一定的时间才能够释放此端口，不设置SO\_REUSEADDR

就无法正常使用该端口。

### 3、ChannelOption.SO\_KEEPALIVE

Channeloption.SO\_KEEPALIVE参数对应于套接字选项中的SO\_KEEPALIVE，该参数用于设置TCP连接，当设置该选项以后，连接会测试链接的状态，这个选项用于可能长时间没有数据交流的

连接。当设置该选项以后，如果在两小时内没有数据的通信时，TCP会自动发送一个活动探测数据报文。

### 4、ChannelOption.SO\_SNDBUF和ChannelOption.SO\_RCVBUF

ChannelOption.SO\_SNDBUF参数对应于套接字选项中的SO\_SNDBUF，ChannelOption.SO\_RCVBUF参数对应于套接字选项中的SO\_RCVBUF这两个参数用于操作接收缓冲区和发送缓冲区

的大小，接收缓冲区用于保存网络协议站内收到的数据，直到应用程序读取成功，发送缓冲区用于保存发送数据，直到发送成功。

### 5、ChannelOption.SO\_LINGER

ChannelOption.SO\_LINGER参数对应于套接字选项中的SO\_LINGER,Linux内核默认的处理方式是当用户调用close（）方法的时候，函数返回，在可能的情况下，尽量发送数据，不一定保证

会发生剩余的数据，造成了数据的不确定性，使用SO\_LINGER可以阻塞close\(\)的调用时间，直到数据完全发送

### 6、ChannelOption.TCP\_NODELAY

ChannelOption.TCP\_NODELAY参数对应于套接字选项中的TCP\_NODELAY,该参数的使用与Nagle算法有关

Nagle算法是将小的数据包组装为更大的帧然后进行发送，而不是输入一次发送一次,因此在数据包不足的时候会等待其他数据的到了，组装成大的数据包进行发送，虽然该方式有效提高网络的有效

负载，但是却造成了延时，而该参数的作用就是禁止使用Nagle算法，使用于小数据即时传输，于TCP\_NODELAY相对应的是TCP\_CORK，该选项是需要等到发送的数据量最大的时候，一次性发送

数据，适用于文件传输。
