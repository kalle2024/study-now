# 初识Spring Cloud
## 1、架构演进
> 单体架构

![单体架构](images/单体架构.png)
> 垂直化拆分

![垂直化拆分](images/垂直化拆分.png)

> 集群+负载均衡

![集群负载均衡](images/集群负载均衡.png)

> SOA：Service Oriented Architecture

![SOA架构](images/SOA架构.png)

> 微服务

![微服务](images/微服务.png)

> Service Mesh 服务网格的解决方式

> Istio<br>
> 所有的网络通信问题，流量进出都可以使用Proxy<br>
> Proxy组件的管理：服务注册与发现、配置管理、安全认证等等

![Istio](images/Istio.png)

## 2、微服务架构的定义
(1) 微服务结构是一种架构设计风格，本质上是通过多个小的服务开发一个完整的应用`[shop]`<br>
(2) 每个服务都会有自己独立的进程`[jar java进程]`<br>
(3) 这些服务因为被部署在不同的java进程、机器上，所以它们需要进行彼此间的通信`[调用]`，轻量级的通信机制，比如HTTP协议`[其它还可以是计算机网络模型中应用层、传输层的协议，包括对这些协议的封装]`，如BIO、NIO、Netty、Dubbo、Thrift、gRPC等、Http2、RestTemplate、OpenFeign、Okhttp、HttpClient、HttpURLConnection等<br>
(4) 这些服务通过自动化的机制进行部署：jenkins，加上一些容器化，利用资源，方便迁移<br>
(5) 这些服务的集中管理是非常少的<br>
(6) 这些服务可能是通过不同的编程语言开发的`[Java、Go、Python、C++等]` 异构的微服务<br>
(7) 这些服务可能是通过不同的数据库存储技术`[user --> db:mysql  xxx: redis、mongodb、es]`

> 微服务架构下可能需要解决的问题

**基本问题**

(1) 服务注册和发现：注册中心<br>
微服务所在的机器地址可能包括端口号都可能会变化：ip:port<br><br>
(2) 负载均衡
- 随机
- 轮询
- hash
- 最少访问...

(3) 服务调用
- RestTemplate
- OpenFeign
- Dubbo等

**进阶问题**

(4) 服务调用容错：超时、限流、降级、舱壁模式...<br>
(5) 分布式消息异步处理机制<br>
(6) 配置中心：配置统一管理<br>
共享配置，以及更改共享配置<br>
(7) 网关：进行路由规则的配置<br>
客户端访问网关，从而转发到后端的具体服务<br>
安全认证<br>
黑白名单<br>
限流<br>
降低<br>
...<br>

**其他问题**

(8) 分布式锁：跨进程之间的资源竞争互斥问题<br>
zookeeper、redis、etcd等<br>
(9) 分布式事务<br>
(10) 中间件 有状态的中间件<br>
leader follower<br>
leader选举和集群管理：paxos、zab、raft<br>
(11) 链路追踪中间件<br>
sleuth+zipkin、skywalking、pinpoint