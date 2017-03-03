---
title: im
date: 2016-10-19 23:37:22
category: c
---

###

``` bash

    // 当 web_socket 客户端与服务器建立连接并完成握手后会回调此函数
    function onOpen(swoole_websocket_server $svr, swoole_http_request $req)

    // 当服务器收到来自客户端的数据帧时会回调此函数
    function onMessage(swoole_server $server, swoole_websocket_frame $frame)

    object(Swoole\WebSocket\Frame)#10 (4)
    {
        ["fd"]     => int(1)            // 客户端的 socket id
        ["finish"] => bool(true)        // 数据内容
        ["opcode"] => int(1)            
        ["data"]   => string(4) "test"  // 表示数据帧是否完整
    }
    
    // 预先定义常量

        ### 数据帧类型 opcode
          - WEBSOCKET_OPCODE_TEXT       = 0x1，文本数据
          - WEBSOCKET_OPCODE_BINARY     = 0x2，二进制数据

        ### 连接状态      
          - WEBSOCKET_STATUS_CONNECTION = 1，连接进入等待握手
          - WEBSOCKET_STATUS_HANDSHAKE  = 2，正在握手
          - WEBSOCKET_STATUS_FRAME      = 3，已握手成功等待浏览器发送数据帧


    // 向 web_socket 客户端连接推送数据
    function swoole_websocket_server->push(
        int $fd,                // 客户端连接的ID
        string $data,           // 要发送的数据内容
        int $opcode = 1,        // 指定发送数据内容的格式，默认为文本
        bool $finish = true     // 
    )


```

### server

``` bash
    
    // 函数用来获取连接的信息
    function swoole_server->connection_info(int $fd, int $from_id, bool $ignore_close = false)
    array(10) {
        ["websocket_status"] => int(3)

        // 来自哪个 server 端口
        ["server_port"]      => int(9501)                  
        ["server_fd"]        => int(3)                     // 来自哪个 server socket 这里不是客户端连接的 fd
        ["socket_type"]      => int(1)
        ["remote_port"]      => int(63101)                 // 客户端连接的端口
        ["remote_ip"]        => string(12) "27.38.145.60"  // 客户端连接的 ip
        ["from_id"]          => int(0)                     // 来自哪个 reactor 线程
        ["connect_time"]     => int(1477837937)            // 连接到 server 的时间，单位秒
        ["last_time"]        => int(1477837938)            // 最后一次发送数据的时间，单位秒
        ["close_errno"]      => int(0)           
    }

    server_fd    // 来自哪个 server socket 这里不是客户端连接的 fd
    socket_type
    remote_port  // 客户端连接的端口
    remote_ip    // 客户端连接的 ip
    from_id      // 来自哪个 reactor 线程
    connect_time // 连接到 server 的时间，单位秒
    last_time    // 最后一次发送数据的时间，单位秒

```

``` bash

    object(Swoole\WebSocket\Server)#3 (16) {
        ["global":"Swoole\Http\Server":private] => int(0)
        ["connections"]                         => object(Swoole\ConnectionIterator)#2 (0) {}
        ["host"]                                => string(7) "0.0.0.0"
        ["port"]                                => int(9501)
        ["mode"]                                => int(3)
        ["type"]                                => int(1)
        ["ports"]                               => array(1) {
            [0] => object(Swoole\Server\Port)#4 (4) {
                ["host"]    => string(7) "0.0.0.0"
                ["port"]    => int(9501)
                ["type"]    => int(1)
                ["onClose"] => object(Closure)#7 (1) {
                    ["parameter"] => array(2) {
                        ["$wsServer"] => string(10) "<required>"
                        ["$frame"]    => string(10) "<required>"
                    }
                }
            }
        }

        ["onOpen"]    => object(Closure)#5 (1) {
        ["parameter"] => array(2) {
                ["$wsServer"] => string(10) "<required>"
                ["$request"]  => string(10) "<required>"
            }
        }

        ["onMessage"] => object(Closure)#6 (1) {
            ["parameter"] => array(2) {
                ["$wsServer"] => string(10) "<required>"
                ["$frame"]    => string(10) "<required>"
            }
        }

        ["onClose"] => object(Closure)#7 (1) {
            ["parameter"] => array(2) {
                ["$wsServer"] => string(10) "<required>"
                ["$frame"]    => string(10) "<required>"
            }
        }

        ["setting"] => array(5) {
            ["open_http_protocol"]      => bool(true)
            ["open_mqtt_protocol"]      => bool(false)
            ["open_eof_check"]          => bool(false)
            ["open_length_check"]       => bool(false)
            ["open_websocket_protocol"] => bool(true)
        }

        ["master_pid"]  => int(3673)
        ["manager_pid"] => int(3674)
        ["worker_id"]   => int(0)
        ["taskworker"]  => bool(false)
        ["worker_pid"]  => int(3676)
    }

```


