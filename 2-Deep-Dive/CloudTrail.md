# 什么是 AWS CloudTrail？
WS CloudTrail 是一项 AWS 服务，可帮助您对 AWS 账户进行操作和风险审核、监管和合规性检查。用户、角色或 AWS 服务执行的操作将记录为 CloudTrail 中的事件。事件包括在 AWS Management Console、AWS Command Line Interface 和 AWS 开发工具包和 API 中执行的操作。

创建时，将在AWS账户上启用 CloudTrail。当您的 AWS 账户中发生活动时，该活动将记录在 CloudTrail 事件中。您可以通过转到 Event history（事件历史记录）轻松查看 CloudTrail 控制台中的近期事件。要持续记录 AWS 账户中的活动和事件，请创建事件数据存储或创建跟踪。有关 CloudTrail 定价的更多信息，请参阅 AWS CloudTrail 定价。

您的 AWS 账户活动的可见性是安全和运营最佳实践的重要方面。您可以使用 CloudTrail 来查看、搜索、下载、归档、分析和响应您的 AWS 基础设施中的账户活动。您可以确定谁或哪个组件对哪些资源执行了哪些操作、事件发生的时间以及其他细节，来帮助您分析和响应 AWS 账户中的活动。或者，您可以对跟踪启用 AWS CloudTrail 见解以帮助您识别和应对异常活动。

您可将 CloudTrail 集成到使用 API 的应用程序、为您的组织自动创建跟踪、检查您创建的事件数据存储和跟踪的状态，以及控制用户查看 CloudTrail 事件的方式。

| 比较  | CloudWatch |   CloudTrail |
| :------------- | :----------: | ------------: |
| 监控方向  | 一个针对AWS资源和应用的监控服务，报告应用程序日志，是一个接近实时的系统事件流，描述了你的AWS资源的变化的服务 |  一项网络服务，记录你的AWS账户中的API活动，提供关于AWS账户中发生的具体信息，是一个更注重在你的AWS账户中进行的AWS API调用的服务  |
| 基本操作  | 默认为您的资源提供免费的基本监控，如EC2实例、EBS卷和RDS DB实例 |  当创建AWS账户时，CloudTrail也被默认启用  |
| 能力  | 可收集和跟踪指标，收集和监控日志文件，并设置警报 |  记录了谁提出了请求、使用的服务、执行的操作、操作的参数以及AWS服务返回的响应元素等信息，然后存储到指定位置  |
|  监控频率 | 在基本监控中以 5 分钟为周期交付指标数据，在详细监控中以 1 分钟为周期交付指标数据；其日志代理默认每五秒发送一次日志数据 |   在 API 调用后 15 分钟内提供事件 |


## AWS CloudTrail
- Provides governance, compliance and audit for an AWS account
- CloudTrail is enabled by default
- CloudTrail provides a history of events/API calls made within an AWS account from:
    - AWS Console
    - SDK
    - CLI
    - AWS services
- Logs from CloudTrail can be put into CloudWatch Logs
- If a resource is deleted in AWS, CloudTrail should contain trace of the operation
- CloudTrail records account activity and service events from most AWS services and logs the following records:
    - The identity of the API caller
    - The time of the API call
    - The source IP address of the API caller
    - The request parameters
    - The response elements returned by the AWS service -Trails can be configured to log data events and management events:
    - **Data events**: These events provide insight into the resource operations performed on or within a resource. These are also known as data plane operations
    - **Management events**: Management events provide insight into management operations that are performed on resources in your AWS account. These are also known as control plane operations. Management events can also include non-API events that occur in the account