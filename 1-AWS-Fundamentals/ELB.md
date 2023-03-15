# [Elastic Load Balancing 定价](https://aws.amazon.com/cn/elasticloadbalancing/pricing/?nc=sn&loc=3)

# Elastic Load Balancing 功能
## **产品比较** 

您可以根据应用程序按需选择合适的负载均衡器。如果您需要灵活管理应用程序，建议您使用 Application Load Balancer。如果应用程序需要实现极致性能和静态 IP，建议您使用网络负载均衡器。如果您的现有应用程序构建于 EC2-Classic 网络内，则您应使用 Classic Load Balancer。

| 功能				 | Application Load Balancer |   Network Load Balancer |   网关负载均衡器 |   Classic Load Balancer |
| :------------- | :----------: | ------------: |------------: |------------: |
| 负载均衡器类型 |  第 7 层 | 第 4 层|第 3 层网关 + 第 4 层负载均衡|第 4/7 层|
| 目标类型 |  IP、实例、Lambda | IP、实例、Application Load Balancer|IP、实例||
| 终止流/代理行为 | 是 | 是 | 否 | 是 |
| 协议侦听器 | HTTP、HTTPS、gRPC | TCP、UDP、TLS | IP | TCP、SSL/TLS、HTTP、HTTPS |

## **安全性** 

使用 Amazon Virtual Private Cloud (VPC) 时，您可以创建和管理与 Elastic Load Balancing 关联的安全组，从而为 Application Load Balancer 和 Classic Load Balancer 提供更多联网和安全选项。您可以将任何负载均衡器配置为面向 Internet，也可创建一个没有公有 IP 地址的负载均衡器，将其用作内部（非面向 Internet 的）负载均衡器。
				
## **高可用性**                 
Elastic Load Balancer 具有高度可用性。您可以在单个可用区或多个可用区中的 Amazon EC2 实例之间分配传入流量。Elastic Load Balancer 会根据应用程序传入流量自动扩展其请求处理容量。为确保您的目标可用且运行状况正常，Elastic Load Balancer 会以可配置的节奏对目标进行运行状况检查。

## **高吞吐量**  
Elastic Load Balancer 旨在处理不断增长的流量，并可以对每秒数百万个请求进行负载均衡。它还可以处理突发的不稳定流量模式。

## **运行状况检查**
Elastic Load Balancer 仅将流量路由至 EC2 实例、容器、IP 地址、微服务、Lambda 函数和设备等运行状况正常的目标。借助 Elastic Load Balancing，您可以通过以下两种方式更好地了解应用程序的运行状况：(1) 运行状况检查改进建议，支持您配置详细错误代码。通过运行状况检查，您可以监控与负载均衡器关联的各个服务的运行状况；(2) 新指标，让您了解 EC2 实例上运行的各个服务的流量。

## **粘性会话**
粘性会话是将同一客户端的请求路由至同一目标的一种机制。Elastic Load Balancers 支持粘性会话。粘性在目标组级别进行定义。

## **运行监控和日志记录**
Amazon CloudWatch 将报告 Application Load Balancer 和 Classic Load Balancer 的各项指标，例如请求数量、错误数量、错误类型和请求延迟等等。Amazon CloudWatch 还会跟踪 Network Load Balancer 和网关负载均衡器的各项指标，例如活动流量计数、新流量技术、处理的字节数等等。Elastic Load Balancers 还与 AWS CloudTrail 集成，后者可跟踪至 ELB 的 API 调用。

# AWS学习笔记
## 传统负载均衡器（Classic Load Balancer）
- Class Load Balancer可以将入向流量自动分布到多个健康的EC2实例上
- ELB是最终用户的唯一接触点
- ELB本身就是一个绝对高可用，永不宕机的分布式软件，**用户不需要考虑ELB的高可用性，不需要为其设计高可用的架构设计** 而且ELB不是单点故障
- ELB具有弹性，能自动对自身进行性能的提升，即可以理解为ELB能处理无穷无尽的数据请求
    - 但ELB的弹性不是立马生效的，如果应用程序在某个时间点有爆发性的流量发生（比方说淘宝双11），那么ELB是不会马上进行扩容的，扩容的过程需要一定的时间（1到7分钟）
    - 如果有可预料的爆发性流量要发生（或者需要进行压力测试），那么可以联系AWS技术支持，告诉AWS流量预计发生的开始和结束时间、预计的每秒请求数、总请求数。AWS可以对该ELB进行预热（pre-warm）从而提前达到能处理这些流量的性能大小
- ELB是阻挡来自网络攻击的第一道防线（比如DDoS攻击）
- 你不需要为ELB打补丁，或管理和维护它的操作系统
- 能分担加密和解密的工作，从而减少EC2实例的系统负担
- 能和AWS弹性伸缩（Auto Scaling）集成，从而能保证后台运行的EC2实例能满足流量的需求
- 默认情况下，ELB的流量转发规则是 TCP 侦听器使用轮询路由（Round Robin）算法，对 HTTP 和 HTTPS 侦听器使用最少未完成请求路由算法。
- ELB只在一个特定的AWS区域中工作，**不能跨区域（Region），但可以跨可用区（AZs）**
- 基于ELB在所处应用架构中的位置不同，可以分两个类型ELB
    - **Internet Load Balancer** – 是面向公网的负载均衡器，能接受来自Internet用户的连接请求
    - **Internal Load Balancer** – 是面向AWS私有网段的负载均衡器，一般仅服务于AWS内部的资源。典型的使用案例是放置在前端服务器和后端服务器之间

## DNS解析
- ELB会以DNS (Domain Name System)的形式显示在AWS管理控制台，并且会动态解析不同公网IP地址，我们在使用ELB时要尽量用DNS来对它进行访问，而不是IP地址
- 在ELB进行弹性扩容的时候，它的DNS记录会被更新，DNS会解析到新的IP地址上（因此这也是上面所说的我们要尽量用DNS名来访问ELB）
- DNS记录的TTL时间是60秒
- 建议客户端（程序）每60秒更新DNS查找记录，以获取最新的ELB地址和最好的ELB性能

## 健康检查（Health Check)
ELB在每一个健康检查间隔（HealthCheck Interval）都会向所有已注册的实例发送基于Ping、端口或者（网页）路径的检查数据包，并且在响应超时（Response Timeout）这个时间内等待实例的回复。如果连续没有得到回复的次数超过定义的不健康阈值（Unhealthy Threshold），那么这个实例会被标记为OutofService。如果在连续得到实例回复的次数超过了健康阈值（Healthy Threshold）的话，那么这个实例会被重新标记为Inservice状态。
- ELB会对所有注册到这个ELB上的EC2实例进行健康检查，无论目前的健康状态如何
- ELB的监控状态分别为InService（表示健康）或者OutofService（表示不健康）

## 监听器（Listeners）
- Listeners可以用来监听用户对ELB发起的请求，以及ELB和后台EC2实例之间的请求
- Listeners可以定义监听的协议和端口
- Listeners支持HTTP, HTTPS, SSL, TCP协议

## 连接耗尽（Connection Draining）
默认情况下，一个已注册再ELB的EC2实例取消了注册或者进入OutofService状态，那么ELB会马上切断这个实例正在进行的连接。

为了保证Classic Load Balancer中当有实例变成不健康的状态（OutofService）或者正在取消注册，而该实例上已经建立的连接不受影响， 请启用Connection Draining功能。它能保证该不健康的实例在处理完所有已有的连接请求之后，才真正地从ELB内去除，接着ELB不会再转发请求给这个实例。

Connection Draining的可设置时间限制范围是1~3600秒（默认为300秒）。当达到这个最大时限时，不管当前实例是否处理完请求，ELB都会强制关闭与这个实例的连接。

## 粘性会话/会话关联（Sticky Sessions/Session Affinity）
默认情况下，Classic Load Balancer会将每一个用户请求转发到负载最小的已注册实例上。但是如果启用Sticky Sessions /Session Affinity，则在会话期间ELB会将来自某个用户的所有请求都转发到同一个实例上。

## 应用程序负载均衡器（Application Load Balancer）
应用程序负载均衡器（Application Load Balancer）工作在7层（应用层），因此也被称为7层的ELB。

在应用程序负载均衡器中，引入了规则这个概念。ELB在收到请求之后，会按照优先顺序评估侦听器的规则，然后根据定义的规则将流量转发到特定的目标组中。如下图所示，你可以配置不同的侦听器规则，然后根据流量的内容或者URL路径来将不同的请求转发到不同的目标组内，而一个目标组又包含了若干的目标（EC2实例)。


应用程序负载均衡器在其他方面和上文讲的传统负载均衡器非常类似，那他们有什么大的区别呢？

- Application Load Balancer可以进行基于路径的路由。即可以根据用户请求中的URL字段不同来将请求发送到不同的目标组中。比方可以定义ELB，将访问https://iteablue.com/posts/*文章的流量转发到目标组1中，然后将访问https://iteablue.com/pages/*页面的流量转发到目标组2中，那么就可以把原本的一个网页应用程序分解成更小的服务单元
- ALB可以侦听HTTP数据包头部的信息，根据此字段来定义规则
- ALB支持通过IP地址进行目标注册，包括位于VPC之外的目标。即可以在一个ALB中定义4个AWS中的EC2实例，同时定义2个来自公司内网的物理服务器
- 支持容器化的应用程序

## 网络负载均衡器（Network Load Balancer）
网络负载均衡器（Network Load Balancer）工作在4层（传输层），因此也被称为4层的ELB。

- NLB可以基于协议、源 IP 地址、源端口、目标 IP 地址、目标端口和 TCP 序列号，使用流式哈希算法选择目标。
- NLB可以每秒处理数百万个请求
- 支持静态IP地址用于负载均衡器
- 同ALB一样，NLB支持通过IP地址进行目标注册，包括位于VPC之外的目标
- 支持容器化的应用程序



# Elastic Load Balancers
## Scalability and High Availability
- Scalability means that an a system can handle greater loads by adapting
- We can distinguish two types of scalability strategies:
    - Vertical Scalability (scale up/down)
        - Increase the size of the current instance (ex. from a t2.micro instance migrate to a a t2.large one)
        - Vertical scalability is common for non distributed systems, such as databases
        - RDS, ElastiCache are services that can scale vertically
    - Horizontal Scalability (scale out/in)
        - Increase the number of instances on which the application runs
        - Horizontal scaling implies having a distributed system
        - It's easy to scale horizontally thanks to could offerings such as EC2
- High Availability means running our application in at least 2 data centers (AZs)
    - The goal of high availability is to survive a data center loss
- High Availability can be:
    - Passive
    - Active
- Load balancers can scale but not instantaneously - contact AWS for a "warm-up"
- Troubleshooting:
    - 4xx errors are client induced errors
    - 5xx errors are application induced errors (server side errors)
    - Error 503 means that the load balancer is at capacity or no registered targets can be found
    - If the load balancer can't connect to the application, it most likely means that the security group blocks the connection
- Monitoring:
    - ELB access logs will log all the access requests to the LB
    - CloudWatch Metrics will give aggregate statistics (example: connections counts)