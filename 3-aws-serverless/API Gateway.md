# API Gateway
Amazon API Gateway 是一项AWS服务，用于创建、发布、维护、监控和保护任意规模的 REST、HTTP 和 WebSocket API。API 开发人员可以创建能够访问 AWS 或其他 Web 服务以及存储在 AWS 云中的数据的 API。作为 API Gateway API 开发人员，您可以创建 API 以在您自己的客户端应用程序中使用。或者，您可以将您的 API 提供给第三方应用程序开发人员。

API Gateway 创建符合下列条件的 RESTful API：

- 基于 HTTP 的。

- 启用无状态客户端-服务器通信。

- 实施标准 HTTP 方法例，如 GET、POST、PUT、PATCH 和 DELETE。

## API Gateway 的功能
Amazon API Gateway 提供如下功能：

- 支持有状态 (WebSocket) 和无状态（HTTP 和 REST）API。

- 强大且灵活的身份验证机制，如 AWS Identity and Access Management 策略、Lambda 授权方函数和 Amazon Cognito 用户池。

- 用以安全地推出更改的金丝雀版本部署。

- CloudTrail 记录和监控 API 使用情况和 API 更改。

- CloudWatch 访问日志记录和执行日志记录，包括设置警报的能力。有关更多信息，请参阅使用 Amazon CloudWatch 指标监控 REST API 执行 和 使用 CloudWatch 指标监控 WebSocket API 执行。

- 能够使用 AWS CloudFormation 模板以支持创建 API 有关更多信息，请参阅 Amazon API Gateway 资源类型参考和 Amazon API Gateway V2 资源类型参考。

- 支持自定义域名。

- 与 AWS WAF 集成，以保护您的 API 免遭常见 Web 漏洞的攻击。

- 与 AWS X-Ray 集成，以了解和分类性能延迟。

## 请求如何路由到业务逻辑
https://zhuanlan.zhihu.com/p/375528758


## 为什么需要API Gateway

在微服务的架构模式下，API Gateway是微服务架构中一个非常通用的模式，利用API Gateway可以解决调用方如何调用独立的微服务这个问题。
从部署结构上说，上图是不采用API Gateway的微服务部署模式，我们可以清晰看到，这种部署模式下，客户端与负载均衡器直接交互，完成服务的调用。但这是这种模式下，也有它的不足。

### 不足

不支持动态扩展，系统每多一个服务，就需要部署或修改负载均衡器。

无法做到动态的开关服务，若要下线某个服务，需要运维人员将服务地址从负载均衡器中移除。

对于API的限流，安全等控制，需要每个微服务去自己实现，增加了微服务的复杂性，同时也违反了微服务设计的单一职责原则。

### 优点

采用API Gateway可以与微服务注册中心连接，实现微服务无感知动态扩容。

API Gateway对于无法访问的服务，可以做到自动熔断，无需人工参与。

API Gateway可以方便的实现蓝绿部署，金丝雀发布或A/B发布。

API Gateway做为系统统一入口，我们可以将各个微服务公共功能放在API Gateway中实现，以尽可能减少各服务的职责。

帮助我们实现客户端的负载均衡策略。


## Endpoint Types
1. **Edge-Optimized (default)**: for global clients
- Requests are routed through the CloudFormation Edge locations
- The API Gateway still lives in only one region
2. **Regional**:
- For clients within the same region
- Could manually be combined with CloudFront having more control over caching strategies and distributions
3. **Private**:
- Can only be accessed from a VPC using an ENI
- We can use resource policies to define access