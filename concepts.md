[toc]

## concept

### dns

1. dns 是全网域名和 ip 地址的映射

### cdn

### domain 域名相关

1. 记录类型
   - CNAME: 指向另外一个域名
   - A 类地址: 指向一个 IP 服务器
   - `*.a.hubby.top`
   - 隐性 URL 等
2. A 类域名添加过程
   - a.hubby.top --> A 记录 --> a.hubby.top 所在的 DNS 服务器
   - 用户 --> 访问 a.hubby.top --> 用户所在的 DNS 服务器 --> 找 a.hubby.top 所在的 DNS 服务器

### arp: Address Resolution Protocal

1. arp 是**同一局域网**内 ip 和网卡硬件地址的映射

   ![avatar](/static/image/layers/dl-arp-flow.png)
   ![avatar](/static/image/layers/dl-arp-flow2.png)

2. arp 包含的 mac 地址只可能是局域网内的目标地址或者路由网关的 MAC{流向公网}
3. arp 内的 IP 与 MAC 的映射在开机时是空的, 后续学习补充上来的
4. 局域网 arp 建表过程:

   - A 查本地 ARP 表发现 B 的 IP 和 MAC 映射关系不存在
   - A 通过 ARP**⼴播**的形式向局域⽹发出消息, 询问某 IP 对应的 MAC 地址是多少
     1. ⽐如 A 此时知道 B 的 IP, 但不知 B 的 MAC, 就在**局域⽹**内发起**ARP ⼴播**询问局域⽹下**所有机器**, 哪个机器的 IP 与 B 的 IP ⼀致
   - B 收到这个 ARP 消息, 发现 A 要问的 IP 与⾃⼰的 IP ⼀致, 就会把⾃⼰的 MAC 地址作为应答返回给 A
   - 其他机器由于 IP 地址不符, 则忽略
   - 此时 A 就知道了 B 的 MAC 地址, 顺便把消息记录到本地 ARP 表⾥, **下次直接⽤表⾥的关系就⾏**， 不需要每次都去问

### uri

1. 统⼀资源标识符, URL 是 URI 的⼦集才对

### url

1. 统⼀资源定位符

### rtt{Round-Trip Time}

1. 往返时延

### [rst](https://blog.csdn.net/ndrg55/article/details/121107647)

1. 用来关闭异常的连接, 是 TCP 包头中的标志位

### socket

### lan(Local Area Network): 局域网

### 路由器

### 集线器: 物理层

1. 数据{输⼊的信号}复制到 N 个端⼝后, 对应转发到 N 台机器⾥

   ![avatar](/static/image/concept/concept-hub.png)

### 交换机: 数据链路层(二层) + `无MAC地址{不是目的地} + 有MAC地址映射表`

![avatar](/static/image/layers/network-s-rl.png)

1. 集线器的广播不好: 机器多了广播数据量太大, 浪费⽹络资源
2. 交换机作用: A 发消息给 B, 且不转发给 C
3. 实现: `交换机内部维护了⼀张MAC地址表{学习}`
4. **MAC 地址表**: `1号端口是交换机的端口`
   - A 发消息到交换机, 交换机发现是从其 1 号端口进来的
   - 则会在 MAC 地址表上, 记录 A 的 MAC 地址对应 1 号端口
   - 长时间不使用会被释放映射
5. mac 表建立好之后:
   - A 发送消息给 B: 数据包会包含 B 的 MAC 地址作为目标 MAC 地址
   - 交换机从端 1 收到 A 发送的数据, 将目标 mac 地址提取, 与 MAC 地址表对比
   - 发现 B 的 MAC 地址正好在 2 号端口, 那么就把数据转发给 2 号端口
6. 特例 2:
   - MAC 地址的目标标端口和这个包的源端口是同⼀个端口: 丢弃
   - mac 地址表里没有则广播

![avatar](/static/image/concept/concept-switch.png)

### ⽹桥:

1. 可以理解为两个⽹线⼝的交换机{将两台电脑桥接在一起}
2. 交换机则是多⽹线⼝的**⽹桥**, 可以把多台电脑给连(桥接)起来

### 路由器(三层交换机)

1. 原因: 交换机只能在局域网内工作 + 不可能让交换机记住全网设备的 MAC 地址{不现实}
2. 因此发明了路由器, 在网络层, 有 IP 的引入, 可以在网络间传输转发
   ![avatar](/static/image/concept/concept-router.png)
3. 静态路由 + 动态路由

### 路由器 vs 交换机

1.  路由器内一般有交换机
2.  mac 地址区别
    - 路由器每个⽹⼝下都有⼀个 MAC 地址和 IP 地址;
    - 交换机没有 MAC 地址(永远不可能是目标地址)
3.  转发: `于⽹络规模的⼤⼩`
    - 交换机: 交换机在 MAC 地址表⾥找不到转发端⼝时会选择⼴播
    - 路由器: 在无法匹配路由规则时会丢弃数据包, 并通过 ICMP 告知发送发
4.  学习
    - 交换机可以学习: arp(数据链路层) + mac 地址表的学习{不广播, 针对性转发}
    - 路由器: 路由规则多是需要手动配置的

### IP(点分字节): `⽹络号+主机号`

![avatar](/static/image/layers/ip-byte.png)

1. 路由表: 转发消息到对应的 IP(下一跳)`{什么样的消息该转发到什么端口}`

### tcp/udp{视频推流}

### 光猫: 光调制解调器{光电信号转换}

![avatar](/static/image/concept/concept-cat.png)
