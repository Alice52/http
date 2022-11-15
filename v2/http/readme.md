[toc]

## introduce

1. spec

   - [rfc-2022](https://www.ietf.org/rfc/rfc9110.txt)
   - [rfc-http1](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.2)

2. http: 无状态

   - url: `restful-api`
   - headers
   - method: 8 种
   - status code
     1. 1xx: 提示信息{请求已收到继续处理}
     2. 2xx: 成功
     3. 3xx: 重定向
     4. 4xx: 客户端错误
     5. 5xx: 服务端错误

3. https: http +ssl(tls)

4. version

   - http/1.0
   - http/1.1
   - http/2.0
   - http/3.0: tcp 废弃

## comparison with grpc

| grpc                          | rest                   |
| ----------------------------- | ---------------------- |
| proto buffer: smaller, faster | json: slower, lager    |
| HTTP/2: lower latency         | HTTP/1: high latency   |
| bi/directional & async        | C/S only               |
| stream support                | Req/Res mechanism only |
| API oriented, no constraints  | CRUD oriented          |
| rpc based                     | http based             |
