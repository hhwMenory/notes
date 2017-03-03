---
title: java socket
date: 2017/2/22 23:10:50
category: java
---

``` bash

    # InetAddress
    # Url
    # socket

    ## tcp 协议是面向连接、可靠的、有序的，以字节流的方式发送数据

    Server                                 Client
    建立服务端侦听socket
    等待并接收连接请求                      创建连接socket 向服务端发送请求
    接收请求后 创建连接socket
                                开始通信
                              双方关闭资源

    ** 可以使用多线处理侦听到 socket 链接 **

    ## udp(用户数据包协议) 协议是无连接、不可靠的、无序的

        - 以数据报(Datagram)作为数据传输的载体
        - DatagramPacket: 表示数据报包
        - DatagramSocket: 进行端到端通信的类


    ### Server

        1. DatagramSocket 侦听端口
        2. 创建数据报来接受客户端数据
        3. 接受数据 (阻塞接收)
        4. 读取数据 Byte[] ===> String

    ### Client

        1. 创建数据报
        DatagramPacket packet = new DatagramPacket(data, data.length, address, port);
        2. 发送数据
        DatagramSocket socket = new DatagramSocket();
        socket.send(packet);

```
