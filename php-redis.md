### 用php源码实现与redis的连接  

- Redis是典型的C/S架构软件，Client和Server之间通过TCP连接进行通信。TCP是传输层，通信是在应用层。与redis的通信协议和http协议一样，都是建立在TCP连接之上。  
- 原则上，只要是支持socket的编程语言都可以用来编写Redis的客户端。在php里，使用stream_socket_client来建立与redis服务所对应的套接字的连接。  
- 要与redis进行通信并正确地发送读取数据，需要先了解redis客户端和服务端之间的通信协议，简称RESP(REdis Serialization Protocol)
- 协议的一大特点是所有命令和数据以 "\r\n" 结尾。
按照协议的规范，格式化请求的命令，或整理接收到的数据，即可实现redis的客户端。