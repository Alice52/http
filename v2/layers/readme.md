[toc]

## 网络模型

![avatar](/static/image/layers/network-layer.png)
![avatar](/static/image/layers/network-layer-detail.png)

1. osi 七层模型: 前三层在用户态 + 后四层在内核态

   - 应用层: http/ftp/ssh/dns/[pop3/smtp/imap]
   - 表示层: telnet/snmp
   - 会话层: smtp
   - 传输层: tcp/udp
   - 网络层: ip/icmp
   - 数据链路层: **arp**/fddi/ethernet
   - 物理层: ieee 802.1a

2. tcp/ip 四层模型

   - 应用层
   - 传输层
   - 网络层: **arp**
   - 数据链路层

3. 应用层
4. 表示层
5. 会话层
6. 传输层: 源/目标端口 + 握手连接{3/4} + 挥手断连{4/2}

   ![avatar](/static/image/layers/table-transfer.png)
   ![avatar](/static/image/layers/network-layer-net.png)

   - `链接表: netstat -anpt`
   - TCP: 字节流 + 安全可靠 + 面向连接
     ![avatar](/static/image/layers/tcp-header.png)
   - UDP: 视频推流
     ![avatar](/static/image/layers/udp-header.png)

7. 网络层: 源/目标 IP + 可以跨网络

   - `路由表: route -n`
   - 查找下一跳地址: 如何走
     ![avatar](/static/image/layers/table-network.png)
   - 报文头
     ![avatar](/static/image/layers/ip-deader.png)

8. 数据链路层: 源/目标 MAC 地址 + 不能跨网络

   - `ip&mac映射表: arp -a`, 获取下一跳的 MAC 地址
   - arp 是同一局域网内 ip 和网卡硬件地址的映射
     ![avatar](/static/image/layers/table-datalink.png)
   - arp 协议在 tcp/ip 模型中属于网络层, 在 osi 模型中属于链路层
   - 报文: 源和⽬的 MAC 地址
     ![avatar](/static/image/layers/dl-message.png)

9. 物理层: ⽐特流
   - 从数据链路层到物理层, 数据会被转为 01 ⽐特流
10. 应用: 交换机 & 路由器

    ![avatar](/static/image/layers/network-s-rl.png)

## 数据传输

1. 数据包

   - 传输层: `源端口号 --> 目标端口号`
   - 网络层: `源IP地址 --> 目标IP地址`, tcp/ip 找到下一跳的 IP(**找路**)
   - 数据链路层: `源mac地址 --> 目标mac地址`: mac 地址解决节点之间(**执行走**)

   ![avatar](/static/image/layers/network-message.png)
   ![avatar](/static/image/layers/network-layer-tcpip.png)

2. http 报文
