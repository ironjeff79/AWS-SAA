#   AWS Lambda
[什么是 AWS Lambda？ - AWS Lambda] (https://docs.aws.amazon.com/zh_cn/lambda/latest/dg/welcome.html)
Lambda 是一项计算服务，可使您无需预置或管理服务器即可运行代码。Lambda 在可用性高的计算基础设施上运行您的代码，执行计算资源的所有管理工作，其中包括服务器和操作系统维护、容量调配和弹性伸缩和记录。借助 Lambda，您可以为几乎任何类型的应用程序或后端服务运行代码。您只需要以 Lambda 支持的一种语言提供您的代码。

## 应在何时使用 Lambda？
**Lambda 函数有三个主要组件：触发器、代码和配置。**
Lambda 是很多应用程序场景的理想计算服务，只要您可以在 Lambda 标准运行时环境和 Lambda 提供的资源中运行应用程序代码。


使用 Lambda 时，您只负责您的代码。Lambda 管理提供内存、CPU、网络和其他资源均衡的计算机群，以运行代码。由于 Lambda 管理这些资源，因此您无法在提供的运行时上登录计算实例或自定义操作系统。Lambda 代表您执行操作和管理活动，包括管理容量、监控并记录 Lambda 函数。


如果您需要管理自己的计算资源，AWS 还提供了其他计算服务以满足您的需求。例如：
- Amazon Elastic Compute Cloud (Amazon EC2) 提供多种 EC2 实例类型可供选择。它能让您自定义操作系统、网络和安全设置以及整个软件堆栈。您将负责预置容量、监控服务器队列的运行状况和性能，并通过部署可用区来增强容错能力。

- 您可使用 AWS Elastic Beanstalk 将应用程序部署和扩展到 Amazon EC2 上。您将保留对底层 EC2 实例的所有权和完全控制权。

## Lambda 功能
以下关键功能可帮助您开发可扩展、安全且易于扩展的 Lambda 应用程序：

- **并发和扩展控制** 
并发和扩展控制（如并发限制和预置并发）使您可以精细控制生产应用程序的扩展和响应能力。

- **定义为容器映像的函数**
使用首选的容器镜像工具、工作流程和依赖项来构建、测试和部署 Lambda 函数。

- **代码签名**
Lambda 的代码签名提供了信任和完整性控件，您可用来验证 Lambda 函数中是否只部署获得批准的开发人员发布的未更改的代码。

- **Lambda 扩展**
您可以使用 Lambda 扩展来增强您的 Lambda 函数。例如，使用扩展程序可以更轻松地将 Lambda 与您喜欢的工具集成，用于监控、观察、安全和管控。

- **函数蓝图**
函数蓝图提供了示例代码，演示如何将 Lambda 与其他AWS服务或第三方应用程序结合使用。蓝图包括 Node.js 和 Python 运行时的示例代码和函数配置预设。

- **数据库访问**
数据库代理管理数据库连接池并从函数中继查询。这使得函数能够在不耗尽数据库连接的情况下达到高并发级别。

- **文件系统访问**
您可以配置函数以将 Amazon Elastic File System (Amazon EFS) 文件系统挂载到本地目录。借助 Amazon EFS，您的函数代码可以安全且高并发地访问和修改共享资源。
