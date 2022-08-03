# common-http

1. this is common repo about http.

## outline

1. 七层⽹络

   - 每一层的协议: lvs

2. 相关概念

   - tcp/udp{视频推流}
   - ip
   - dns
   - cdn
   - http
   - https
   - ssl / tls
   - 对称加密{aes/des/des3} & 非对称加密{rsa}
   - 摘要算法: sha256/md5

3. http: 无状态

   - url: `restful-api`
   - headers
   - method: 8 种
   - status code

     1. 1xx: 提示信息{请求已收到继续处理}
     2. 2xx: 成功
     3. 3xx: 重定向
     4. 4xx: 客户端错误
     5. 5xx: 服务端错误

4. https: http +ssl(tls)

5. version

   - http/1.0
   - http/1.1
   - http/2.0
   - http/3.0: tcp 废弃

6. 安全

   - dos
   - csrf

7. 应用

   - 跨域: cros
   - restful api

8. [常见问题列表](https://github.com/Alice52/common-http/issues/8)

## network

1. 两台电脑可以通过⼀根⽹线直接连接进⾏通信
2. 机器变多, 可以把⽹线都接到集线器{物理层}上: 无脑⼴播
3. 拒绝⼴播, 可以⽤⼆层交换机{数据链路层}: 学习⽣产`MAC地址表`, 知道消息发到哪
4. MAC 地址超多, 交换机 MAC 地址表放不下, 改⽤路由器{⽹络层}: 在网络间传输
5. 路由器和光猫之间是好搭档, 光猫负责把光纤⾥的光信号转换成电信号给路由器
6. 现在⼤部分路由器也⽀持交换机的功能: 所以家⾥的台式机电脑⼀般就连到⼀个路由器, 再连个光猫就够能上⽹
