## introduce

1. http: Hypertext Transfer Protocol

   - Hypertext: 能够进行分支判断(response's alert)和差异响应的文本(比如文字可以点击, 可以触发脚本执行, 可以调用服务端)
   - 超媒体: 能够进行分支判断和差异响应的文本, 图形, 电影和声音的复合体
   - 超文本/超媒体意味着**信息和控制的同时呈现**, 使得信息成为用户/自动机通过其获得**选择和选择动作**的可供性

2. spec

   - [rfc-2022](https://www.ietf.org/rfc/rfc9110.txt)
   - [rfc-http1](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.2)

## comparison with grpc

| grpc                          | rest                   |
| ----------------------------- | ---------------------- |
| proto buffer: smaller, faster | json: slower, lager    |
| HTTP/2: lower latency         | HTTP/1: high latency   |
| bi/directional & async        | C/S only               |
| stream support                | Req/Res mechanism only |
| API oriented, no constraints  | CRUD oriented          |
| rpc based                     | http based             |
