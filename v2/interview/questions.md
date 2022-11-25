[toc]

## 2. 沾包问题

1. 粘包这个问题的根因是由于开发⼈员没有正确理解 TCP **⾯向字节流的数据传输⽅式**, 本身并不是 TCP 的问题, 是开发者的问题
2. TCP 会沾包: ` tcp 组装分割数据包 + 无边界标识`
   - 基于字节流把数据发到接收端: 可能包含上⼀次想要发的数据的部分信息
   - 接收端根据需要在消息⾥加上识别消息边界的信息, 不加就可能出现粘包问题
   - TCP 粘包跟 Nagle 算法有关系: 但关闭 Nagle 算法并不解决粘包问题
3. UDP 不会粘包: `每次发送一个完整消息 + 有长度标识{都在在udp receiver buffer 中还是会粘连}`
   - 是基于数据报的传输协议: 每次都是穿一个完整的数据包{不会切割组装}
   - UDP 头中有长度信息: 防止应用层读取不及时导致的在 udp rev buffer 中的粘连
4. IP: `只会拆包, 但不会将不同的分包组装成一个发送` + `拆分后的数据包具有相同header和各自的offset`
   - IP 层也切⽚, 但是因为不关⼼消息⾥有啥, 因此有不会有粘包问题

## 3. http vs rpc(grpc)

1. [TDB](https://mp.weixin.qq.com/s/d3DNfcyBjb8ayKq5AcvePQ)

---

## reference

1. [常见问题列表](https://github.com/Alice52/common-http/issues/8)
