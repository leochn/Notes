---
title: windows下强制杀死进程
date: 2018-11-30 15:45:05
tags: [windows,tool]
---
## windows下强制杀死进程
```
window下当使用某个端口时，发现这个端口被占用，但是正规的关闭这个进程又关闭不了，可以使用强制杀死。
```

<!-- more -->

比如想查看8088端口被哪个进程占用了，cmd下输入这个命令：netstat   -ano|findstr 8088

如下图:

![windows](/assets/images/tools/windows-001.png)


找到这个端口的占用PID后，就可以杀死这个进程，用下面的命令：

查找哪个程序的进程PID是13828:

tasklist | findstr 13828

杀死PID进程:

taskkill /pid 13828 -t -f

![windows](/assets/images/tools/windows-002.png)



## netstat
说明：显示协议统计和当前 TCP/IP 网络连接。其相关命令行参数如下：
```
 -a            显示所有连接和侦听端口。
 -b            显示在创建每个连接或侦听端口时涉及的可执行程序。
               在某些情况下，已知可执行程序承载多个独立的
               组件，这些情况下，显示创建连接或侦听端口时涉
               及的组件序列。此情况下，可执行程序的名称
               位于底部[]中，它调用的组件位于顶部，直至达
               到 TCP/IP。注意，此选项可能很耗时，并且在您没有
               足够权限时可能失败。
 -e            显示以太网统计。此选项可以与 -s 选项结合使用。
 -f            显示外部地址的完全限定域名(FQDN)。
 -n            以数字形式显示地址和端口号。
 -o            显示拥有的与每个连接关联的进程 ID。
 -p proto      显示 proto 指定的协议的连接；proto 可以是下列任
               何一个: TCP、UDP、TCPv6 或 UDPv6。如果与 -s 选
               项一起用来显示每个协议的统计，proto 可以是下列任
               何一个: IP、IPv6、ICMP、ICMPv6、TCP、TCPv6、UDP
               或 UDPv6。
 -r            显示路由表。
 -s            显示每个协议的统计。默认情况下，显示
               IP、IPv6、ICMP、ICMPv6、TCP、TCPv6、UDP 和 UDPv6
               的统计；-p 选项可用于指定默认的子网。
 -t            显示当前连接卸载状态。
 interval      重新显示选定的统计，各个显示间暂停的间隔秒数。
               按 CTRL+C 停止重新显示统计。如果省略，则 netstat
               将打印当前的配置信息一次。
如：

netstat –ano
说明：以数字形式显示所有链接和侦听端口（地址和端口号），-o表示显示进程id（PID）
```


## tasklist

在netstat的基础上，我们可以利用tasklist显示在本地或远程机器上当前运行的进程列表.

说明：用findstr是为了进行字符串过滤，类似于Linux中的grep.

## taskkill
使用该工具按照进程 ID (PID) 或映像名称终止任务。
```
如：

C:\Users\Administrator.WIN7-1609051925>taskkill /F /pid 944

成功: 已终止 PID 为 944 的进程。

说明:  /F    指定强制终止进程。
       /PID  processid   指定要终止的进程的 PID。
```
注意：终止任务可能需要管理员权限，若是用dos操作，需要“以管理员身份启动”cmd窗口。
