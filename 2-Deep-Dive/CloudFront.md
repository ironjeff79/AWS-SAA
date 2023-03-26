# 什么是 Amazon CloudFront？
Amazon CloudFront 是一项加快将静态和动态 Web 内容（例如 .html、.css、.js 和图像文件）分发给用户的速度的 Web 服务。CloudFront 通过全球数据中心（称作边缘站点）网络传输内容。当用户请求您用 CloudFront 提供的内容时，请求被路由到提供最低延迟（时间延迟）的边缘站点，从而以尽可能最佳的性能传送内容。

- 如果该内容已经在延迟最短的边缘站点上，CloudFront 将直接提供它。

- 如果内容不在边缘站点中，CloudFront 将从已定义的源（例如，已确定为内容最终版本的来源的 Amazon S3 存储桶、MediaPackage 通道或 HTTP 服务器，如 Web 服务器）检索内容。

例如，假设您要从传统的 Web 服务器中提供图像，而不是从 CloudFront 中提供图像。例如，您可能会使用 URL https://example.com/sunsetphoto.png 提供图像 sunsetphoto.png。

您的用户可以轻松导航到该 URL 并查看图像。但他们可能不知道其请求从一个网络路由到另一个网络（通过构成互联网的相互连接的复杂网络集合），直到找到图像。

CloudFront 通过 AWS 主干网络将每个用户请求传送到能以最佳方式提供您的内容的边缘站点，以此来加速分发您的内容。通常，这是向查看器提供传输最快的 CloudFront 边缘服务器。使用 AWS 网络可大大降低用户的请求必须经由的网络数量，从而提高性能。用户将会体验到延迟 (加载文件的第一个字节所花费的时间) 更短、数据传输速率更高。

您还会获得更高的可靠性和可用性，因为您的文件（也称为对象）的副本现在存储（或缓存）在全球各地的多个边缘站点上。

## 如何设置 CloudFront 以提供内容
您创建 CloudFront 分配，以告知 CloudFront 您希望内容从何处传输，并告知有关如何跟踪和管理内容传输的详细信息。然后，当有人想查看或使用内容时，CloudFront 使用靠近您的查看器的计算机（边缘服务器）快速传输内容。

1. 您指定源服务器（如 Amazon S3 存储桶或您自己的 HTTP 服务器），CloudFront 将从该服务器获取您的文件，这些文件随后将从全世界的 CloudFront 边缘站点分配。

源服务器将存储您的对象的原始最终版本。如果您通过 HTTP 提供内容，您的源服务器将为 Amazon S3 存储桶或 HTTP 服务器，例如，Web 服务器。您的 HTTP 服务器可以在 Amazon Elastic Compute Cloud (Amazon EC2) 实例上运行，也可以在您管理的服务器上运行；这些服务器也称*为自定义源*。

2. 您将您的文件上传至您的源服务器。您的文件也称为对象，通常包括网页、图像和媒体文件，但可以是可通过 HTTP 提供的任何内容。

如果您将 Amazon S3 存储桶用作源服务器，则可以将存储桶中的对象设为公开可读，这样知道这些对象的 CloudFront URL 的任何人都可以访问它们。您还可以选择将对象设为私有，并控制哪些人可以访问它们。

3. 创建一项 CloudFront 分配，此项分配将在用户通过您的网站或应用程序请求文件时告诉 CloudFront 从哪些源服务器获取您的文件。同时，您还需指定一些详细信息，如您是否希望 CloudFront 记录所有请求以及您是否希望此项分配创建后便立即启用。

4. CloudFront 为新分配指定一个域名，您可以在 CloudFront 控制台中查看该域名，该域名也可能被返回以响应编程请求（例如 API 请求）。如果您愿意，您可以添加要改用的备用域名。

5. CloudFront 将您的分配的配置（而不是您的内容）发送到其所有边缘站点或节点 (POP) – 它们是位于地理位置分散的数据中心（CloudFront 在其中缓存您的文件的副本）内的服务器的集合。

您在开发网站或应用程序时，需使用 CloudFront 为您的 URL 提供的域名。例如，如果 CloudFront 返回 d111111abcdef8.cloudfront.net 作为您的分配的域名，则 Amazon S3 存储桶中（或 HTTP 服务器上的根目录中）的 logo.jpg 的 URL 将为 https://d111111abcdef8.cloudfront.net/logo.jpg。

或者，您可以设置 CloudFront 对您的分配使用您自己的域名。在这种情况下，URL 可能是 https://www.example.com/logo.jpg。

（可选）您可配置您的源服务器以向文件添加标头，表示您希望文件在 CloudFront 边缘站点的缓存中保留的时长。默认情况下，每个文件在边缘站点中保留 24 个小时后即会过期。最小过期时间为 0 秒；没有最大过期时间。

## CloudFront 使用案例
### 加快静态网站内容分发速度
CloudFront 可以加快将静态内容（例如，图像、样式表、JavaScript 等）分发给全球范围内的查看器的速度。通过使用 CloudFront，您可以充分利用 AWS 主干网络和 CloudFront 边缘服务器以在查看器访问您的网站时为其提供快速、安全、可靠的体验。

存储和交付静态内容的简单方式是使用 Amazon S3 存储桶。将 S3 与 CloudFront 结合使用可获得许多好处，包括可以选择使用源访问控制来轻松限制对您的 S3 内容的访问。

### 提供点播视频或实时流视频
CloudFront 提供了多个选项来将媒体流式传输到全球查看器 – 预先录制的文件和实时内容。

对于点播视频 (VOD) 流，您可以使用 CloudFront 以常见格式（如 MPEG DASH、Apple HLS、Microsoft 平滑流和 CMAF）将内容流式传输到任何设备。

对于广播实时流，您可以在边缘站点缓存媒体片段，以便将按正确顺序传输片段的清单文件的多个请求组合起来，从而减小源服务器的负载。

### 在整个系统处理过程中加密特定字段
在对 CloudFront 配置 HTTPS 时，您已获得与源服务器的安全的端到端连接。在添加字段级加密时，您可以在整个系统处理过程中保护特定的数据并实施 HTTPS 安全，以便只有源中的某些应用程序可以查看数据。

要设置字段级加密，您可以将公有密钥添加到 CloudFront，然后指定要使用该密钥加密的字段集。

### 在边缘进行自定义
通过在边缘站点上运行无服务器代码，开启了为查看器自定义内容和体验的很多可能性，并减少了延迟。例如，您可以在源服务器停机进行维护时返回自定义错误消息，查看器不会获得一般 HTTP 错误消息。或者，您可以在 CloudFront 将请求转发到您的源之前，使用函数来帮助向用户授权并控制对您的内容的访问。

将 Lambda@Edge 与 CloudFront 配合使用，可以通过多种方式自定义 CloudFront 提供的内容。

### 使用 Lambda@Edge 自定义提供私有内容
除了使用已签名的 URL 或已签名的 Cookie 之外，还可使用 Lambda@Edge 帮助您配置 CloudFront 分配以提供来自您自己的自定义源的私有内容。

要使用 CloudFront 提供私有内容，请执行以下操作：

- 要求用户（查看器）使用已签名的 URL 或已签名的 Cookie 来访问内容。

- 限制对源的访问，以便只能从 CloudFront 的面向源的服务器上进行访问。为此，可以执行以下操作之一：

    - 对于 Amazon S3 源，您可以使用源访问控制 (OAC)。

    - 对于自定义源，您可以执行以下操作：

        - 如果自定义源受 Amazon VPC 安全组或 AWS Firewall Manager 保护，您可以使用 CloudFront 托管式前缀列表，以便仅允许从 CloudFront 面向源的 IP 地址传入到源的流量。

        - 使用自定义 HTTP 标头将访问限制为仅来自 CloudFront 的请求。有关更多信息，请参阅 在自定义源上限制对文件的访问和向源请求添加自定义标头。

        - 如果自定义源需要自定义访问控制逻辑，则可以使用 Lambda@Edge 来实现该逻辑。

## Q&A
### Amazon CloudFront 可以用来做什么?

Amazon CloudFront 提供简单的 API，让您能够：

- 使用遍布全球的边缘站点网络来处理请求，从而以低延迟和高数据传输速率来分发内容。
- 无需就合同和最低承诺进行谈判，即可开始使用。

### 如何使用 Amazon CloudFront?

要使用 Amazon CloudFront，您必须按以下步骤操作：

- 对于静态文件，请将最终版本的文件存储在一个或多个原始服务器上。它们可能是 Amazon S3 存储段。对于动态生成的个性化或自定义内容，您可以使用 Amazon EC2 或其他任何 Web 服务器作为原始服务器。这些原始服务器将存储或生成将通过Amazon CloudFront 分发的内容。

- 通过简单的 API 调用在 Amazon CloudFront 上注册您的原始服务器。此调用将返回一个 CloudFront.net 域名，您可以使用该域名，通过 Amazon CloudFront 服务从您的原始服务器分发内容。例如，您可以注册 Amazon S3 存储段“bucketname.s3.amazonaws.com”作为所有静态内容的来源，并注册一个 Amazon EC2 实例“dynamic.myoriginserver.com”作为所有动态内容的来源。然后，使用 API 或 AWS 管理控制台，您可以创建可能返回“abc123.cloudfront.net”作为分配域名的Amazon CloudFront 分配。

- 将 cloudfront.net 域名或您创建的 CNAME 别名包括在您的 Web 应用程序、媒体播放器或网站中。使用 cloudfront.net 域名（或您设置的 CNAME）发出的每个请求，都被路由到最适合以最高性能分发内容的边缘站点。该边缘站点将尝试使用文件的本地副本来处理请求。如果本地副本不可用，Amazon CloudFront 将从源文件中获取副本。然后，此副本将能够在该边缘站点使用，以便处理今后的请求。

### Amazon CloudFront 如何提供更高性能?

Amazon CloudFront 采用边缘站点和区域性边缘缓存的全球网络，可缓存您的内容副本以更靠近读者。Amazon CloudFront 确保将由距离最近的边缘站点来处理最终用户请求。由此，传输读者请求的距离变短，Amazon CloudFront 也为读者提升了性能。对于没有缓存在边缘站点和区域性边缘缓存上的文件，Amazon CloudFront 将与您的原始服务器保持永久连接，以便尽快从原始服务器提取这些文件。最后，Amazon CloudFront 使用其他优化措施（例如更广的 TCP 初始拥塞窗口），在将您的内容传输至查看者时提供更高的性能。

### Amazon CloudFront 如何降低通过 Internet 分配内容的成本？

与其他 AWS 产品一样，Amazon CloudFront 没有最低承诺，您只需为自己的服务用量付费。与自托管相比，Amazon CloudFront 无需您运行分布在 Internet 上多个站点的缓存服务器网络，从而避免了相关开支和复杂性，也无需您过高预置容量以便处理可能出现的流量峰值。Amazon CloudFront 还运用了多种技术，例如，将在一个边缘站点上针对同一文件发出的多个同步查看者请求重叠到向原始服务器发出的单个请求中。这样可以降低原始服务器上的负载，从而减少扩展原始基础设施的需求，实现进一步成本节省。

### Amazon CloudFront 与 Amazon S3 有何不同？

Amazon CloudFront 是分发经常访问的静态内容的理想之选，可从边缘站点传输中受益 – 例如常用的网站图像、视频、多媒体文件或软件下载。