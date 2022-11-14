[toc]

![avatar](/static/image/common/http-overview.png)

## layout

1. introduce

   - osi
   - concept

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
