# 6.11. Service Discovery 服务发现

在微服务架构中，服务之间是存在依赖的。例如在订单系统中创建订单时，需要对用户信息做快照，这时候也就意味着这个流程要依赖: 订单、用户两个系统。当前大型网站的语境下，多服务分布式共存，单个服务也可能会跑在多台物理/虚拟机上。所以即使你知道你需要依赖的是“订单服务”这个具体的服务，实际面对的仍然是多个 ip+port 组成的集群。因此你需要: 1. 通过“订单服务”这个名字找到它对应的 ip+port 列表；2. 决定把这个请求发到哪一个 ip+port 上的订单服务。

ip+port 的组合往往被称为 endpoint。通过“订单服务”去找到这些 endpoint 的过程，叫做服务发现。选择把请求发送给哪一台机器，以最大化利用下游机器的过程，叫做负载均衡。本节主要讨论服务发现。

## 故障节点摘除