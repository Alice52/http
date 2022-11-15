[toc]

## api

1. 简介

   - 应用程序接口: 预先定义的接口**用于**应用的通信
   - 本质: 是一组定义、程序及协议的集合(无需知道实现细节也能实现声明的功能)
   - 和语言无关, 理论上具有网络操作能力的所有编程语言都可以提供 api 服务

2. pros

   - 快速**扩展**功能
   - 提高开发**效率**: 避免造轮子
   - 降低模块之间的**耦合**度

3. api flow

   ![avatar](/static/image/common/api/api-flow.png)

4. api style

   ![avatar](/static/image/common/api/api-style.png)

## 前后端分离

1. 前后端依赖严重耦合, 不能适应独立快速开发
2. 全栈工程师的难得
3. 前端技术的模块化, 可以独立开发部署
4. 前端的独立为后面的服务分布式, 微服务及动态扩容提供了基础
5. 前端 code[node] +server

---

## rest-ful

1. [detail](./01.restful.md)
2. core point

   - core: 抽象资源 + 面向资源设计
   - rest 不是银弹, 其表达能力其实有限: 完全达到 rest 所有指导原则的系统非常困难(比如不同 Vo | 资源不明确 | 多资源 | 动作性的操作)
   - 具体 api 设计可以参考 GitHub 的 API 设计: **`资源 | 动词(非标准 rest 但是实用)`**

## graphql

1. [detail](./02.graphql.md)
2. core point: `1+1+3+2`

   - summary: 在客户端和服务器之间转移合约的 api: $\color{#FF0000}{表述服务器具有的能力 + 客户端描述需求=功能产品}$
   - intros: `将 Vo 前置到前段 + Dto 自校验` + `带宽 + 请求数量 + 灵活 + subscribe` + cons
   - _pros_: 字段及类型自校验, 但是自定义消息不友好
   - pros-带宽请求: 类型表述的资源有层级关系, 可以客户端决定获取字段 + 多重资源在同意请求中获取
   - pros-灵活: 由 graphql 服务进行组装响应返回 + 每个字段都可以对应 resolver
   - cons: 性能 + `N+1` + 学习使用成本

## graphql & restful _& soap_

1. [graphql](#graphql)

   - pros: **`将 Vo 前置到前段 + Dto 自校验`**
   - pros: 带宽 + 请求数量 + 灵活
   - pros: [subscription] 接受服务端的推送
   - cons-N+1: 可以通过 DataLoader 异步查询聚合成一条语句解决
   - cons-性能: sql 字段要全选以供 resolver, 不能重复利用覆盖索引等特性`{内存和 CPU 不值钱, 是可以接受的}`
   - cons-使用: 需要预先创建 api schema[强类型]

2. [restful](#rest-ful)

   - intros: 统一接口 | 无状态 | 缓存 | BS 结构 |服务端向客户端提供可执行代码的能力
   - **`HATEOAS 才是 REST 的关键功能`** + REST 是针对 API 的最高级别的抽象和最佳模型
   - pros: 客户端和服务端的解耦 | 可发现性 | 缓存友好
   - cons-api 数量: 在应用领域模型超复杂时具有很大弊端: 不同 vo + 关联数据导致的 api 数量与管理间的矛盾
   - cons-带宽: 庞大的负载

3. diff

   - 概念上
     1. rest: 是一种风格, 没有 spec, 有一些指导原则, 但实际上并不受任何强制的约束
     2. graphql: 是一种语言, 是规范, 有对应的 spec 的, 存在 graphql-server 负责构建响应
   - (**带宽**)核心概念: `对数据粒度的控制(fileds 可以但是不友好)`
     1. rest: url 区分资源(最小控制粒度)
     2. graphql: 类型(模式{m/q/s})区分资源, 关心的是资源中的字段(最小控制粒度)
   - (**关联**)资源与其获取方式相分离:
     1. rest: [服务端决定一切返回], 一个资源与获取它的方式是耦合的(比如获取图书信息就是后端写死的逻辑)
     2. graphql: [客户端决定一切返回], 分层是数据是前端控制并获取的, 不是服务端替我们决定的(比如前端主动获取 book 关联的作者等灵活信息)
   - (**资源**)处理流程
     1. rest: 一个请求对应一个路由处理器处理(内部可以操作多个资源)
     2. graphql: 一个 graphql 的请求可以唤起多个解析器
   - 响应
     1. rest: 服务端完全自定义响应
     2. graphql: 由查询方指定结构, **之后由 graphql 进行构建组装的**
   - 请求方式
     1. rest: get | post | put | delete
     2. graphql: post
   - (**请求数量**)api 数量: 关联数据|不同 vo
     1. rest: 很多(为了实现不同的关联数据 || 为了返回不同的 vo 会更多{fields 不友好})
     2. graphql: 1 个, 分层资源会在 resolver 自动检索
     ```json
     // 此时 rest api 就遇到困难: creator 是否显示{标识参数 | 每次都返回(流量) | 通过新api返回 creator(项目维护)}
     {
       "name": "zack",
       "creator": {
         "id": 2,
         "level": 1
       }
     }
     ```
   - 请求校验
     1. rest: 规范层没有校验, 但是可以在 spring 生态下校验并完成**自定义消息**
     2. graphql: 规范层面自校验, 不易自定义错误提示
   - sql 语句 & 性能: `现在服务器内存和 CPU 不值钱, 是可以接受的`
     1. rest: 能充分利用覆盖索引等特性进行优化
     2. graphql:[n+1 问题] SQL 查询必须对应的类型的所有字段以供选择, 否则就会报错
   - 开发过程中向后兼容
     1. rest: 不需要的字段也会返回占用带宽等资源
     2. graphql: 自向后兼容, 不需要的字段不操作就相当于不存在
   - 调试 & 文档
     1. rest: postman | swagger
     2. graphql: Altair-GraphQL-Client(_graphiql_) | introspection
   - 生态
     1. rest: spring 的支持(全局异常处理{自定义异常 code} | 预处理{权限}等)支持友好
     2. graphql: [dgs 可以预处理{auth}等, 但是不是很友好](https://graphql.cn/learn/authorization/)
   - 服务端推流
     1. rest: 长链接可以做到
     2. graphql: subscription

4. same

   - 都是基于 http 的无状态的语言无关的**数据交换**的设计风格: 但 graphql 明确的 spec{存在 graphql server 层(负责构建返回响应)}, 但是 rest 没有
   - 都有资源的概念, 只是 graphql 中叫到类型
   - 都响应 json

5. _soap_
   - intros: 只支持 xml 数据交换协议, 支持有状态和无状态消息传
   - pros: 独立于语言和平台 | 绑定到各种协议 | 内置错误处理 | **安全**拓展
   - cons: 大量的消息结构(不是有效内容) | 重量级

---

## reference

1. [rest vs graphql](https://www.cnblogs.com/chenwenhao/articles/12687763.html)
2. [(rest|graphql) || (rpc|http)](https://mp.weixin.qq.com/s/d3DNfcyBjb8ayKq5AcvePQ)
