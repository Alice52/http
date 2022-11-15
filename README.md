[toc]

![avatar](/static/image/common/http-overview.png)

## layout

1. [introduce](/v2/layers/readme.md)

   - osi
   - [concept](/v2/layers/readme.md)

2. layers: 7(4)

   - application layer: http/ftp/ssh/dns/[pop3/smtp/imap]
   - _representation layer_: telnet/snmp
   - _session layer_: smtp
   - transport layer: tcp/udp
   - network layer: ip/icmp
   - data-link layer: **arp**/fddi/ethernet
   - _physical layer_: ieee 802.1a

3. **http**: application layer

   - http: status + connection + method + header + cache
   - https: http + ssl
   - http1 | 2 | 3(quic)

4. security

   - 中间人攻击
   - ddos 攻击
   - csrf
   - cros
   - 防盗链

5. tools

   - wireshark | ssh | proxy | fiddler
   - postman/swagger/apifox
   - altair graphql client | graphiql

6. performance & apply

   - netty
   - socket programming
   - nginx tcp optimize

7. interview & production case

   - network io: epoll
   - performance optimize: network
   - rpc | http
   - graphql | rest | soap

## network evolution

1. 两台电脑可以通过⼀根⽹线直接连接进⾏通信
2. 机器变多, 可以把⽹线都接到集线器{物理层}上: 无脑⼴播
3. 拒绝⼴播, 可以⽤⼆层交换机{数据链路层}: 学习⽣产`MAC地址表`, 知道消息发到哪
4. MAC 地址超多, 交换机 MAC 地址表放不下, 改⽤路由器{⽹络层}: 在网络间传输
5. 路由器和光猫之间是好搭档, 光猫负责把光纤⾥的光信号转换成电信号给路由器
6. 现在⼤部分路由器也⽀持交换机的功能: 所以家⾥的台式机电脑⼀般就连到⼀个路由器, 再连个光猫就够能上⽹
