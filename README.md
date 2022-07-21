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
